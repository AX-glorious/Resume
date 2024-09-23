<template>
    <div class="page d-flex flex-column align-items-start ">
        <AboutPage id="about"/>
        <EducationPage id="education"/>
        <SkillPage id="skill"/>
        <ProgressExperience id="progress"/>
        <HobbiesPage id="hobby"/>
        <ContactPage id="contract"/>
    </div>
    
</template>


<script setup>
import { onMounted,ref } from 'vue';
import AboutPage from './sessionDeatil/AboutPage.vue';
import ContactPage from './sessionDeatil/contactPage.vue';
import EducationPage from './sessionDeatil/educationPage.vue';
import HobbiesPage from './sessionDeatil/hobbiesPage.vue';
import ProgressExperience from './sessionDeatil/progressExperience.vue';
import SkillPage from './sessionDeatil/skillPage.vue';

const activeSection = ref('');
const observerOptions = {
    root: document.querySelector('.page'),
    rootMargin: '0px 0px 100px 0px',
    threshold: 0.1 // 10% 可见性
};

const observerCallback = (entries) => {
    entries.forEach(entry => {
        console.log(entry.target.id, entry.isIntersecting);//打印观察对象
        if (entry.isIntersecting) {
            activeSection.value = entry.target.id;
            // 派发事件通知 SideNavPC 组件
            window.dispatchEvent(new CustomEvent('activeSectionChange', { detail: { sectionId: entry.target.id } }));
        }
    });
};

onMounted(() => {
    const observer = new IntersectionObserver(observerCallback, observerOptions);
    
    // 观察各个 section
    const sections = ['about', 'education', 'skill', 'progress', 'hobby', 'contract'];
    sections.forEach(id => {
        const section = document.getElementById(id);
        if (section) {
            observer.observe(section);
        }
    });
});
</script>

<style scoped>
.page{
    max-height: 100vh;
    overflow-y: auto;
}
</style>