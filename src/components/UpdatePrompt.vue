<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
const baseURL = import.meta.env.VITE_APP_BASE_URL;
const prompt = ref('');
const router = useRouter();

const emit = defineEmits(['update-start', 'update-end']);

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

    emit('update-start');

    const id = await sendRequest();

    emit('update-end');

    console.log(prompt.value);
    router.push(`/planner/${id}`).then(() => router.go());
};
</script>

<template>
    <div class="box">
        <form @submit="handleSubmit">
            <textarea type="text" id="prompt" v-model="prompt" required></textarea>
            <div class="buttons">
                <button class="button-submit" type="submit">C'est parti</button>
                <button class="button-exemple" @click="router.push(`/`)">Voir l'historique</button>
            </div>
        </form>
    </div>
</template>
