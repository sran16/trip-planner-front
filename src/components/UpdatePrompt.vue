<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';


const baseURL = import.meta.env.VITE_APP_BASE_URL;


const prompt = ref('');


const router = useRouter();

// Define the custom events to be emitted
const emit = defineEmits(['update-start', 'update-end']);

// Function to send the update request to the server
const sendRequest = async () => {
    try {

        const id = router.currentRoute.value.params.id;

        // Send a PATCH request to update the planner with the new prompt
        const response = await fetch(`${baseURL}/v1/planners/${id}`, {
            method: 'PATCH',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ prompt: prompt.value })
        });

        const data = await response.json();
        // Return the updated planner ID
        return data.id;
    } catch (error) {
        console.error(error);
    }
};

// Function to handle the form submission
const handleSubmit = async (event) => {

    // Prevent the default form submission behavior
    event.preventDefault();

    // Emit the 'update-start' event
    emit('update-start');

    // Send the update request and get the updated planner ID
    const id = await sendRequest();

    // Emit the 'update-end' event
    emit('update-end');

    // Redirect to the updated planner page and refresh the page

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
