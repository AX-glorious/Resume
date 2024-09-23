<template>
    <div class="contract  bg-light border-bottom border-dark">
        <div class="page d-flex flex-column align-items-start">
            <!-- 标题 -->
            <h1 class="title display-5 mb-1 ">
                <span class="text-color ">联系 </span><span class="fw-bold">我</span>
            </h1>
            <hr class="solid-divider ">
            <p class="intro h5 m-2 text-muted">如果您需要，您可以通过以下方式与我取得联系:</p>

            <!-- 内容 -->
            <div class="contract_container my-5">
                <!-- 元素内容 -->
                <div class="contract_item " v-for="(contract, i) in contractData.way" :key="i">
                    <div class="iocn ">
                        <i data-v-a8356e5e="" :class=contract.iconClass></i>
                    </div>
                    <div class="content d-flex flex-column">
                        <div class="title fw-bold text-start">{{ contract.title }}</div>
                        <div class="detail text-muted text-start">{{ contract.content }}</div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>


<script setup>
import axios from 'axios';
import {ref, onMounted } from 'vue';


let contractData=ref({
    way:[]
});

onMounted(()=>{
    axios.get('/data/resumeData/chinese/contractData.json')
    .then(response=>{
        contractData.value=response.data;
        console.log(contractData.value);
        
    })
    .catch(error=>{
        console.error('加载联系方式数据时出错:', error);
    })
})


</script>

<style scoped>
.contract {
    width: 100%;
    .page {
        min-height: 60vh;
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


        .contract_container {
            width: 100%;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;

            .contract_item {
                display: flex;
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
                    background: blueviolet;
                }

                .content {
                    padding: 0 4%
                }
            }
        }
    }
}
</style>