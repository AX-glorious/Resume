<template>
    <div>
        <!-- pc端 -->
        <SideNavPC v-if="isPc" />

        <!-- 移动端 -->
        <SideNavMobile v-else />
    </div>
</template>

<script>
import SideNavPC from './sideNav/SideNavPC.vue';
import SideNavMobile from './sideNav/SideNavMobile.vue';


export default {

    components: {
        SideNavPC, SideNavMobile
    },


    data() {
        return {
            isPc: true, // 默认是PC端
        };
    },
    // mounted() {
    //     this.checkDevice();
    //     window.addEventListener("resize", this.checkDevice);
    // },
    // beforeUnmount() {
    //     window.removeEventListener("resize", this.checkDevice);
    // },
    // methods: {
    //     checkDevice() {
    //         // 简单的判断屏幕宽度，大于 768px 是 PC 端，否则是移动端
    //         this.isPc = window.innerWidth > 768;
    //     },
    // },
};
</script>