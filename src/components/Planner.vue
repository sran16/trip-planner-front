<script setup>
import { ref, onMounted, computed } from 'vue';
import { useRoute } from 'vue-router';
import update from '@/assets/icons/update.svg';

const baseURL = import.meta.env.VITE_APP_BASE_URL;
const data = ref(null);
const route = useRoute();
const id = route.params.id; 

onMounted(async () => {
    try {
        const response = await fetch(`${baseURL}/v1/planners/${id}`);
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
    const planner = data.value.id === id ? data.value : null;
    return planner;
});
</script>
<template>
    <div class="planner">

        <div v-if="filteredData">
            <div class="prompt-update">
                <h4>{{ filteredData.prompt }}</h4>
                <div class="update-icon">
                    <img class="img-update" :src="update" alt="icon-update" />
                </div>
            </div>
            <h5>Itinéraire</h5>
            <ul>
                <li v-for="item in filteredData.itinerary" :key="item.name">
                    <h2>{{ item.name }}</h2>
                    <p>{{ item.description }}</p>
                </li>
            </ul>
        </div>
    </div>
</template>
<style scoped>
.planner {
    background-color: #242321;
    color: white !important;
    padding: 4px 16px;
}

.prompt-update {
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* padding: 8px; */
    border-radius: 8px;
    margin-bottom: 8px;
}


.update-icon {
    background-color: #6D695E;
    ;
    border-radius: 8px;
    padding: 6px;
    align-items: center;
    display: flex;
    justify-content: center;
    text-align: center;

}

.img-update {
    width: 24px;
}

h5 {
    color: #6D695E;
    margin: 0;
    font-size: 14px;
}

p {
    color: #CECECE;
}

ul {
    padding: 0px 16px;
    list-style-type: decimal;
}
</style>