<template>
    <div class="education  bg-light border-bottom border-dark">
        <div class="page d-flex flex-column align-items-start">

            <!--毕业院校  -->
            <h1 class="title display-6 mb-1 ">
                <span class="text-color ">教育 </span><span class="fw-bold">背景</span>
            </h1>
            <hr class="solid-divider ">
            <p class="intro h5 m-2 text-muted fw-bold">我的基本教育背景信息</p>

            <div class="school w-100 my-5 d-flex justify-content-start ">
                <div class="schoolImg  p-2 rounded-circle">
                    <img class="rounded-circle img-fluidimg-fluid" :src=schoolData.schoolImgUrl alt="">
                </div>
                <div class="detail  mx-4 p-2">
                    <div>
                        <h3 class="name fw-bold text-start text-shadow">{{ schoolData.name }}</h3>
                        <h5 class="major  fw-bold text-start">{{ schoolData.major }}</h5>
                        <div class="year  rounded-pill shadow-sm p-2 my-1 fw-bold">
                            {{ schoolData.start }}➔{{ schoolData.end }}
                        </div>
                    </div>
                    <p class="intro fs-6 text-start my-2 ">{{ schoolData.intro }}</p>
                </div>
            </div>

            <!-- 校园经历 -->
            <p class="intro h4 mx-2 text-muted fw-bold"><span class="text-color">校园</span>经历</p>
            <hr class="w-25">
            <!-- 校园经历数据 -->
            <div v-if="schoolData.experice && schoolData.experice.length >= 1">
                <div class="schoolExperice d-flex justify-content-between align-items-center"
                    v-for="(experice, i) in schoolData.experice" :key="i">
                    <div class="expericeLeft d-flex flex-column align-items-start">
                        <div class="year fw-bold text-center p-2 rounded-pill shadow">
                            {{ experice.start}}➔{{ experice.end }}</div>
                        <div class="position fw-bold text-center mt-4 p-2 rounded-pill shadow">
                            {{experice.position }}</div>
                    </div>
                    <div class="content  text-start m-4  shadow rounded-5">
                        <span>{{experice.content }}</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';


const schoolData = ref({
    name: '',
    schoolImgUrl: '',
    major: '',
    start: '',
    end: '',
    intro: '',
    experice: [],
});

onMounted(() => {
    axios.get('/data/resumeData/chinese/educationData.json')
        .then(response => {
            schoolData.value = response.data; // 设置
            console.log(schoolData);

        })
        .catch(error => {
            console.error('加载学校数据时出错:', error);
        });
})
</script>

<style scoped>
.education {
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

        .school {
            .schoolImg {
                img {
                    width: 13vw;
                    box-shadow: 5px 5px 7px rgba(0, 0, 0, 0.2);
                    max-width: 180px;
                    min-width: 120px;
                }
            }

            .year {
                width: 150px;
                background-color: white;
            }
        }

        .schoolExperice {
            width: 100%;

            .expericeLeft {
                width: 25%;
                flex-shrink: 0;

                .year {
                    width: 100%;
                    

                }

                .position {
                    width: 100%;
                    

                }
            }

            .content {
                width: 75%;
                padding: 4% 8%;
                background-color: white;
                
            }
        }
    }
}
</style>