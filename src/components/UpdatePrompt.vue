<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
const baseURL = import.meta.env.VITE_APP_BASE_URL;
const prompt = ref('');
const router = useRouter();

const sendRequest = async () => {
    try {
        const id = router.currentRoute.value.params.id; 
        const response = await fetch(`${baseURL}/v1/planners/${id}`, {
            method: 'PATCH',
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
                <button class="button-exemple"
                    @click="router.push(`/planner/34cc68bd-132e-4a58-8512-d3e4b25b4cd0`)">Voir un exemple</button>
            </div>
        </form>
    </div>
</template>