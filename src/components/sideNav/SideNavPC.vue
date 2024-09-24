<template>
    <div class="sideNav bg-dark d-flex flex-column">
        <div class="navContent ">
            <div class="personInfo mt-5 d-flex flex-column align-items-center">
                <div class="personImg bg-secondary rounded-circle ">
                    <img :src="resumeData.resumeImgUrl" class="rounded-circle p-2" alt="">
                </div>
                <div class="personName fw-bold text-white mt-3 fs-3">
                    <p>{{ resumeData.name }}</p>
                </div>
            </div>

            <!-- 导航栏目 -->
            <nav :offset="70" class="sessionNav d-flex flex-column align-items-start mx-5 px-4 text-white">
                <a href="#" @click="scrollToSection(nav.href)"
                    :class="['navButton', 'nav-link', 'm-2', 'p-1', { active: activeSection === nav.href }]"
                    v-for="(nav, i) in navData" :key="i">
                    <i :class="nav.icon"></i>
                    <span>&nbsp;&nbsp;&nbsp;{{ nav.text }}</span>
                </a>
            </nav>
        </div>
        <div class="navFooter d-flex align-items-center">
            <a href="https://github.com/AX-glorious?tab=repositories" target="_blank"
                class="icon btn btn-social rounded-circle ms-5  d-flex justify-content-center align-items-center">
                <i data-v-dcc9f2e0="" class="fa-brands fa-github text-white"></i>
            </a>
            <div class="name ms-2 text-white">设计：Aster</div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

// 响应式数据
const resumeData = ref({
    name: '',
    resumeImgUrl: ''
});

const navData = ref([]);

const activeSection = ref('');//接收滚动数据

// 加载数据
onMounted(() => {

    //监听sessionpage的滚动事件，获取当前活跃的session
    window.addEventListener('activeSectionChange', (event) => {
        activeSection.value = event.detail.sectionId
    });

    axios.get('/data/resumeData/chinese/basicData.json')
        .then(response => {
            resumeData.value = response.data;
        })
        .catch(error => {
            console.error('加载简历数据时出错:', error);
        });

    axios.get('/data/resumeData/chinese/navData.json')
        .then(response => {
            navData.value = response.data;
        })
        .catch(error => {
            console.error('加载导航数据时出错:', error);
        });

});

// 点击导航栏滚动到指定页面
const scrollToSection = (sectionId) => {
    const target = document.getElementById(sectionId);
    if (target) {
        target.scrollIntoView({ behavior: 'smooth' });
    }
};

</script>

<style scoped>
.sideNav {
    width: 320px;
    height: 100vh;

    .navContent {
        height: 85vh;

        .personInfo {
            height: 43%;

            .personImg {
                width: 200px;
                height: 200px;

                img {
                    width: 100%;
                }
            }
        }

        .sessionNav {

            .navButton:hover {
                color: rgb(213, 139, 255);
                transition: color 0.4s ease;
            }

            .navButton.active {
                color: rgb(213, 139, 255);
                transition: color 0.4s ease;
            }
        }
    }

    .navFooter {
        height: 15vh;
        .icon {
                width: 70px;
                height: 70px;
                font-size: 40px;
                background-color: #212529;
            }

            .icon:hover {
                background-color:blueviolet;
                transition: color 0.4s ease;

            }
            .name{
                font-size: 18px;
            }
    }
}
</style>