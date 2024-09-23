<template>
    <div class="about container bg-light border-bottom border-dark">
        <div class="page d-flex flex-column align-items-start">
            <h1 class="title display-3 mb-4">
                欢迎来到我的<span class="text-color">简历!</span>
            </h1>
            <div class="d-flex flex-column align-items-start">
                <div class="emil text-color my-1 fs-5">
                    <i data-v-c4644c6f="" class="fa-solid fa-envelope list-item-icon"></i>
                    <span>&nbsp; {{resumeData.email}}</span>
                </div>
                <div class="mobile text-color fs-5">
                    <i data-v-c4644c6f="" class="fa-solid fa-phone list-item-icon"></i>
                    <span>&nbsp; {{resumeData.phone}}</span>
                </div>
            </div>
            <div class="intro text-start my-3">
                <span class="fs-5 text-justify">
                    {{ resumeData.intro }}
                </span>
            </div>
            <div class="iconList my-1 ">
                <a href="https://github.com/AX-glorious?tab=repositories" target="_blank" class="icon btn btn-social bg-dark rounded-circle d-flex justify-content-center align-items-center">
                        <i data-v-dcc9f2e0="" class="fa-brands fa-github text-white"></i>
                </a>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

// 响应式数据
const resumeData = ref({
    intro:'',
    email:'',
    phone:'',
});


onMounted(() => {
    // 加载简历基本信息
    axios.get('/data/resumeData/chinese/basicData.json')
        .then(response => {
            resumeData.value = response.data; // 设置姓名
            // console.log(resumeData.value);
        })
        .catch(error => {
            console.error('加载简历数据时出错:', error);
        });
});

</script>


<style scoped>
.about {
    
    .page {
        height: 100vh;
        padding: 190px 110px;

        .title {
            font-weight: 700;
        }

        .text-color {
            color: blueviolet
        }

        .iconList {
            .icon {
                width: 70px;
                height: 70px;
                font-size: 40px;
                
            }
        }
    }
}
</style>