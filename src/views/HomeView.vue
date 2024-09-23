<template>
  <div class="Page d-flex">
    <SideNav class="flex-shrink-0"/>
      <SessionPage ref="sessionPage" />
  </div>

</template>

<script setup>
// @ is an alias to /src
import SessionPage from '@/components/SessionPage.vue';
import SideNav from '@/components/SideNav.vue';


</script>

<style scoped>

</style>


