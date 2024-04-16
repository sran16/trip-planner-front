<script setup>
import { ref, onMounted } from 'vue';

const data = ref(null);

onMounted(async () => {
    try {
        const response = await fetch('http://localhost:3000/v1/planners');
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        data.value = await response.json();
    } catch (error) {
        console.error(error);
    }
    console.log(data.value);
});
</script>

<template>
    <div>
        <div v-for="(item) in data" >
            <p>{{ item.prompt }}</p>
        </div>
    </div>
</template>