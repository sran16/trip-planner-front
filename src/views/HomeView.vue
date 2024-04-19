<script setup>
import Landing from '@/components/Landing.vue';
import PlannerList from '@/components/PlannerList.vue';
import PromptBox from '@/components/PromptBox.vue';
// import Loading from '@/components/Loading.vue';



</script>

<template>
  <main >
    <!-- <Loading /> -->
    <Landing />
    <PromptBox />
    <PlannerList />
  </main>
</template>
<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
  margin: 0;
}

main.isLoading {
  display: none;
}
</style>
