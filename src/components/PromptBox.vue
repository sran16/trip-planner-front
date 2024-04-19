<script setup>

import { ref } from 'vue';
import { useRouter } from 'vue-router';
import Loading from '@/components/Loading.vue';
const baseURL = import.meta.env.VITE_APP_BASE_URL;
const prompt = ref('');
const router = useRouter();

const isLoading = ref(false);
const sendRequest = async () => {
  try {
    isLoading.value = true;
    const response = await fetch(`${baseURL}/v1/planners`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ prompt: prompt.value })
    });
    const data = await response.json();
    return data.id;
  } catch (error) {
    console.error(error);
  } finally {
    isLoading.value = false;
  }
};

const handleSubmit = async (event) => {
  event.preventDefault();
  const id = await sendRequest();
  router.push(`/planner/${id}`);
};

</script>

<template>
  <div v-if="isLoading">
    <Loading />
  </div>
  <div v-else class="box">
    <form @submit="handleSubmit">
      <textarea type="text" id="prompt" v-model="prompt" required></textarea>
      <div class="buttons">
        <button class="button-submit" type="submit">C'est parti</button>
        <button class="button-exemple" @click="router.push(`/planner/ca15d2cb-7a5f-446e-a3df-cc3261e91912`)">Voir un
          exemple</button>
      </div>
    </form>
  </div>
</template>