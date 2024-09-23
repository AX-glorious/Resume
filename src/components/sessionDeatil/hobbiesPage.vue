<template>
    <div class="hobbies w-100 bg-light border-bottom border-dark">
        <div class="page d-flex flex-column align-items-start">
            <h1 class="title display-5 mb-4 ">
                <span class="text-color ">兴趣</span><span class="fw-bold">爱好</span>
            </h1>
            <hr class="solid-divider ms-1 me-1 mb-3 mb-lg-4">
            <p class="intro h5 text-start text-muted">我对于空闲时间的大概花费</p>

            <!-- 图标区域 -->
            <div class="chartsContainer my-2 mb-5">
                <div id="chartsShow" style="width: 700px;height:400px;"></div>

                <!-- 闲时花销内容 -->
                <div class="hobby d-flex" v-for="(span, i) in hobbyData.span" :key="i">
                    <div class="iocn " :style="{ backgroundColor: span.bgColor }">
                        <i data-v-a8356e5e="" :class=span.iconClass></i>
                    </div>
                    <div class="content d-flex flex-column">
                        <div class="title fw-bold text-start">{{ span.title }}</div>
                        <div class="detail text-muted text-start">{{ span.content }}</div>
                    </div>
                </div>
            </div>

            <!-- 兴趣区域 -->
            <h3 class="title m-2">
                <span class="r fw-bold">兴趣 </span>
                <i class="fa fa-book-open-reader ms-2"></i>
                <hr class="solid-divider w-100 ">
            </h3>
            <div class="hobby_item d-flex m-2 my-2" v-for="(hobby, i) in hobbyData.hobby" :key="i">
                <div class="iocn mx-3">
                    <i data-v-a8356e5e="" :class=hobby.iconClass></i>
                </div>
                <div class="content d-flex flex-column">
                    <div class="title fw-bold text-start">{{ hobby.name }}</div>
                    <div class="detail text-muted text-start">{{ hobby.content }}</div>
                </div>
            </div>

            <!-- 兴趣作品 -->
            <h3 class="title m-2 mt-5 ">
                <span class="r fw-bold">兴趣作品 </span>
                <i class="fas fa-camera"></i>
                <hr class="solid-divider w-100 ">
            </h3>

            <div class="works d-flex">
                <div class="crosswise">
                    <el-carousel :interval="3000" indicator-position="outside" height="34vw" >
                        <el-carousel-item v-for="(work,index) in hobbyData.corsswideWork" :key="index">
                            <div>
                                <img :src=work.ImgUrl alt="">
                            </div>
                        </el-carousel-item>
                    </el-carousel>
                </div>
                <div class="vertical">
                    <el-carousel :interval="3000" indicator-position="outside" height="40vw">
                        <el-carousel-item v-for="(work,index) in hobbyData.verticalWork" :key="index">
                            <div>
                                <img :src=work.ImgUrl alt="">
                            </div>
                        </el-carousel-item>
                    </el-carousel>
                </div>
            </div>
        </div>
    </div>
</template>


<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';
import * as echarts from 'echarts';

let hobbyData = ref({
    span: [],
    hobby: [],
    corsswideWork:[],
    verticalWork:[],
});


onMounted(() => {
    axios.get('/data/resumeData/chinese/hobbies.json')
        .then(response => {
            hobbyData.value = response.data;
            // 准备echarts数据
            const chartData = hobbyData.value.span.map(item => ({
                value: Number(item.percent),
                name: item.title
            }));


            var chartDom = document.getElementById('chartsShow');
            var myChart = echarts.init(chartDom);
            var option;
            option = {

                textStyle: {
                    fontSize: 16, // 设置全局字体大小
                    fontWeight: 600
                },
                tooltip: {
                    trigger: 'item',
                    formatter: function (params) {
                        const total = params.data.value; // 当前项的值
                        const percent = ((total / chartData.reduce((sum, item) => sum + item.value, 0)) * 100).toFixed(0); // 计算百分比
                        return `${params.name}: ${percent}%`; // 显示名称和百分比
                    }
                },
                series: [
                    {
                        name: 'Hobby From',
                        type: 'pie',
                        radius: ['20%', '70%'],

                        itemStyle: {
                            borderRadius: 10,
                            borderColor: '#fff',
                            borderWidth: 2
                        },
                        emphasis: {
                            label: {
                                show: true,
                                fontSize: 35,
                                fontWeight: 'bold'
                            },
                        },
                        labelLine: {
                            show: false
                        },
                        data: chartData
                    }
                ]
            };
            option && myChart.setOption(option);

        })
        .catch(error => {
            console.log("加载兴趣爱好数据出错", error);
        });
});

</script>

<style scoped>
.hobbies {
    .page {
        margin: 30px 30px;
        padding: 60px;

        .text-color {
            color: blueviolet;
            font-weight: 600;
        }

        .solid-divider {
            border: 0;
            width: 20%;
            height: 4px;
            background-color: blueviolet;
            /* 设置线条的颜色 */
            margin-left: 0.25rem;
        }

        .chartsContainer {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;

            .hobby {
                flex-basis: calc(50% - 20px);
                /* 每个组件占一行的 50% 宽度 */
                display: flex;
                padding: 0 2%;

                .iocn {
                    width: 50px;
                    height: 50px;
                    flex-shrink: 0;
                    /* 防止缩小 */
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    font-size: 28px;
                    border-radius: 50%;
                }

                .content {
                    padding: 0 4%
                }
            }
        }

        .hobby_item {
            .iocn {
                width: 50px;
                height: 50px;
                flex-shrink: 0;
                /* 防止缩小 */
                display: flex;
                justify-content: center;
                align-items: center;
                font-size: 28px;
                border-radius: 50%;
                background-color: blueviolet;

            }

        }

        .works {
            width: 100%;
            height: 680px;
            justify-content: space-between;
            gap: 20px;
            .crosswise {
                width: 60%;
                height: 500px;
                aspect-ratio: 16 / 9;
                img{
                    width: 100%;
                }
            }
            .vertical{
                width: 35%;
                aspect-ratio: 16 / 9;
                flex:1;
                img{
                    width: 100%;
                    height: auto;
                }
            }
        }
    }
}
</style>