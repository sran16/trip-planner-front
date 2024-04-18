<script setup>

import { ref } from 'vue';
import { useRouter } from 'vue-router';
const baseURL = import.meta.env.VITE_APP_BASE_URL;
const prompt = ref('');
const router = useRouter();

const sendRequest = async () => {
  try {
    const response = await fetch(`${baseURL}/v1/planners`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ prompt: prompt.value })
    });
    const data = await response.json();
    console.log(data);
    return data.id;
  } catch (error) {
    console.error(error);
  }
};

const handleSubmit = async (event) => {
  event.preventDefault();
  const id = await sendRequest();
  console.log(prompt.value);
  router.push(`/planner/${id}`);
};

</script>

<template>
  <div class="box">
    <form @submit="handleSubmit">
      <textarea type="text" id="prompt" v-model="prompt" required></textarea>
      <div class="buttons">
        <button class="button-submit" type="submit">C'est parti</button>
        <button class="button-exemple" @click="router.push(`/planner/34cc68bd-132e-4a58-8512-d3e4b25b4cd0`)">Voir un
          exemple</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
#prompt {
  background-color: #242321;
  border: 1px solid #6D695E;
  border-radius: 17px;
  height: 14vh;
  width: 80vw;
  margin-bottom: 16px;
  color: #ffffff;
}

.box {
  display: flex;
  justify-content: center;
}

button {
  border-radius: 8px;
  color: #6D695E;
  margin-right: 16px;
  padding: 8px 16px;
}

.button-submit {
  background-color: #6D695E;
  color: #CECECE;
}

.button-exemple {
  background-color: transparent;
  border: 1px solid #6D695E;
  color: #ffffff;
}

.buttons {
  display: flex;
  justify-content: center;
}
</style>