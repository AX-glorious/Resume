<template>
    <div class="skill  flex-grow-1 bg-light border-bottom border-dark">
        <div class="page  d-flex flex-column align-items-start">
            <!-- 标题 -->
            <h1 class="title  display-6 mb-1 ">
                <span class="text-color fw-bold">技能</span>
            </h1>
            <hr class="solid-divider ">
            <p class="intro h4 m-2 text-muted">探索我所掌握和发展的多样技能</p>

            <!-- 技术1 -->
            <div class="teachnology_container ">
                <!-- 技术元素内容 -->
                <div class="teachnology_item d-flex" v-for="(teachnology, i) in skillData.teachnology" :key="i">
                    <div class="iocn ">
                        <i data-v-a8356e5e="" :class=teachnology.iconClass></i>
                    </div>
                    <div class="content d-flex flex-column">
                        <div class="title fw-bold text-start">{{ teachnology.title }}</div>
                        <div class="detail text-muted text-start">{{ teachnology.content }}</div>
                    </div>
                </div>
            </div>

            <!-- 编程能力内容 -->
            <h3 class="title mx-1">
                <span class="r fw-bold">编程</span>
                <i class="fa fa-code ms-2"></i>
                <hr class="solid-divider w-100 ">
            </h3>
            <div class="code_container">
                <div class="codeItem " v-for="(code, i) in skillData.code" :key="i">
                    <div class="icon">
                        <i data-v-a8356e5e="" :class=code.iconClass></i>
                    </div>
                    <div class="content demo-progress">
                        <div class="intro d-flex justify-content-between">
                            <div class="codeeName fw-bold text-muted">{{ code.languageName }}</div>
                            <div class="percent text-muted">{{ code.percent }}%</div>
                        </div>
                        <el-progress :percentage=code.percent :show-text="false" :color="'#8a2be2'" />
                    </div>
                </div>
            </div>

            <!-- 语言内容 -->
            <h3 class="title mx-1 mt-5">
                <span class="r fw-bold">语言</span>
                <i class="fa fa-language ms-2"></i>
                <hr class="solid-divider w-100 ">
            </h3>
            <div class="language_container d-flex flex-column">
                <div class="languageItem d-flex " v-for="(language, i) in skillData.language" :key="i">
                    <div class="country m-4">
                        <img :src=language.img alt="">
                    </div>
                    <div class="content p-1 d-flex flex-column justify-content-center">
                        <div class="name fw-bold text-start">{{ language.languageName }}</div>
                        <div class="intro text-muted">{{ language.intro }}</div>
                    </div>
                </div>
            </div>

            <!-- 附加技能 -->
            <h3 class="title mx-1 mt-5">
                <span class="r fw-bold">附加技能</span>
                <i class="fa fa-marker ms-2"></i>
                <hr class="solid-divider w-100 ">
            </h3>
            <div class="otherSkill_item d-flex m-2" v-for="(otherSkill, i) in skillData.otherSkill" :key="i">
                <div class="iocn mx-3">
                    <i data-v-a8356e5e="" :class=otherSkill.iconClass></i>
                </div>
                <div class="content d-flex flex-column">
                    <div class="title fw-bold text-start">{{ otherSkill.title }}</div>
                    <div class="detail text-muted text-start">{{ otherSkill.content }}</div>
                </div>
            </div>
        </div>
    </div>
</template>


<script setup>
import axios from 'axios';
import { ref, onMounted } from 'vue';

let skillData = ref({
    teachnology: [],
    code: [],
    language: [],
    otherSkill: [],
});


onMounted(() => {
    axios.get('/data/resumeData/chinese/skillData.json')
        .then(respon => {
            skillData.value = respon.data
            console.log(skillData);

        })
})
</script>

<style scoped>
.skill {
    width: 100%;

    .page {
        margin: 30px 30px;
        padding: 60px;

        .text-color {
            color: blueviolet;
            font-weight: 600;
        }

        .solid-divider {
            border: 0;
            width: 10%;
            height: 4px;
            background-color: #8a2be2;
            margin-left: 0.25rem;
        }

        .teachnology_container {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            /* 控制组件间的距离 */
            margin: 5% 0;

            .teachnology_item {
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
                    background-color: blueviolet;
                }

                .content {
                    padding: 0 4%
                }
            }
        }

        .code_container {
            width: 100%;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;

            /* 控制组件间的距离 */
            .codeItem {
                flex-basis: calc(50% - 20px);
                /* 每个组件占一行的 50% 宽度 */
                display: flex;
                padding: 2%;

                .icon {
                    width: 20%;
                    height: 50px;
                    flex-shrink: 0;
                    /* 防止缩小 */
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    font-size: 28px;
                    border-radius: 50%;

                    i {
                        color: blueviolet;
                    }
                }

                .content {
                    width: 80%;

                    .languageName {
                        font-weight: 600;
                    }
                }
            }
        }

        .language_container {
            .languageItem {
                width: 100%;

                .country {
                    width: 7%;

                    img {
                        width: 100%;
                        border-radius: 50%;
                    }
                }
            }
        }

        .otherSkill_item {
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

    }
}
</style>