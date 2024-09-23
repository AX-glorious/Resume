<template>
    <div class=" Progress w-100 bg-light border-bottom border-dark">
        <div class="page d-flex flex-column align-items-start">
            <h1 class="title display-5 mb-5 ">
                <span class="text-color ">项目</span><span class="fw-bold">经历</span>
                <hr class="solid-divider ms-1 me-1 w-50">
            </h1>

            <!-- 项目 -->
            <div class="progressContainer " v-for="(project, i) in progressData.progress" :key="i">
                <div class="text-start h4 fw-bold text-shadow mb-2 ">项目介绍</div>
                <div class="d-flex align-items-center my-4">
                    <div class="introduce ">
                        <h5 class=" text-center fw-bold p-2  rounded-pill shadow">{{ project.name }}</h5>
                        <div class="skill text-center fw-bold p-2 my3 rounded-pill shadow ">{{ project.skill }}</div>
                        <div class="intro text-center fw-bold p-4 my-3 rounded-5 shadow ">{{ project.intro }}</div>
                    </div>

                    <el-carousel :interval="2500" type="card" height="55vw" trigger="click">
                        <el-carousel-item v-for="(imgItem, index) in project.ImgUrl" :key="index">
                            <img :src="imgItem.url" alt="">
                        </el-carousel-item>
                    </el-carousel>
                </div>
                <h4 class="title text-start fw-bold m-2 text-shadow">技术实现</h4>
                
                <div class="accomplishment" v-for="(accomplish,index) in project.accomplish" :key="index">
                    <div class="intro w-100 text-start fw-bold p-4 my-3 rounded-5 shadow ">{{ accomplish.content }}</div>
                </div>
            </div>

        </div>
    </div>
</template>

<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';

let progressData = ref({
    progress: [],
});

onMounted(() => {
    axios.get('/data/resumeData/chinese/progressData.json')
        .then(response => {
            progressData.value = response.data;
            // progressData.value.ImgUrl=response.data.progress.ImgUrl;
            console.log(progressData.value);

        })
        .catch(error => {
            console.error('加载项目数据时出错:', error);
        });
})
</script>

<style scoped>
.Progress {
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


        .progressContainer {
            width: 100%;

            .el-carousel {
                width: 35vw;
                aspect-ratio: 16 / 18; 
            }

            .el-carousel__item {

                img {
                    width: 100%;
                    height: auto;
                }
            }

            .el-carousel__item:nth-child(2n) {
                background-color: #f8f9fa;
            }

            .el-carousel__item:nth-child(2n + 1) {
                background-color: #f8f9fa;
            }

            .introduce {
                width: 45%;
                height: 100%;
                padding-right: 30px;
            }
        }
    }
}
.text-shadow{
    text-shadow: 2px 2px 2px rgba(163, 163, 163, 0.6);
}
</style>