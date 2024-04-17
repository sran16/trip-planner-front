<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';

const data = ref(null);
const route = useRoute();

onMounted(async () => {
    try {
        const response = await fetch('http://localhost:3000/v1/planners');
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const jsonResponse = await response.json();
        
        console.log(jsonResponse);
        data.value = jsonResponse;
    } catch (error) {
        console.error(error);
    }
    console.log(data.value);
});

const filteredData = computed(() => {
    if (!data.value) {
        return null;
    }
    const id = route.params.id;
    const planner = data.value.find(item => item.id === id);
    return planner || null;
});
</script>
<template>
    <div>
        <h4>Itinéraire</h4>
        <div v-if="filteredData">
            <p>{{ filteredData.prompt }}</p>
            <ul>
                <li v-for="item in filteredData.itinerary" :key="item.name">
                    <h2>{{ item.name }}</h2>
                    <p>{{ item.description }}</p>
                </li>
            </ul>
        </div>
    </div>
</template>