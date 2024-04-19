<script setup>
import { ref, onMounted, computed, reactive } from 'vue';
import { useRoute, useRouter } from 'vue-router';

import update from '@/assets/icons/update.svg';
import history from '@/assets/icons/history.svg';
import UpdatePrompt from '@/components/UpdatePrompt.vue';
import Loading from '@/components/Loading.vue';


const baseURL = import.meta.env.VITE_APP_BASE_URL;
const data = reactive({ value: null });
const router = useRouter();
const route = useRoute();
const id = route.params.id;
const showUpdatePrompt = ref(false);
const isLoading = ref(false);

onMounted(async () => {
    try {
        isLoading.value = true;
        console.log(isLoading.value);
        const response = await fetch(`${baseURL}/v1/planners/${id}`);
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const jsonResponse = await response.json();
        console.log(jsonResponse);
        data.value = jsonResponse;
    } catch (error) {
        console.error(error);
    } finally {
        isLoading.value = false;
        
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
const toggleUpdatePrompt = () => {
    showUpdatePrompt.value = !showUpdatePrompt.value;
};
const updateData = (updatedData) => {
    data.value = updatedData;
    showUpdatePrompt.value = false;
    toggleUpdatePrompt();
};
</script>
<template>
    <div class="planner">
        <div v-if="isLoading">
            <Loading />
        </div>
        <div v-else-if="filteredData">
            <div class="prompt-update">
                <h4>{{ filteredData.prompt }}</h4>
                <div class="update-icon">
                    <img @click="toggleUpdatePrompt" class="img-update" :src="update" alt="icon-update" />
                    <img class="img-update" :src="history" alt="icon-history" @click="router.push(`/`)" />
                </div>
            </div>
            <UpdatePrompt v-if="showUpdatePrompt" @update="updateData" />
            <h5>Itinéraire</h5>
            <ul>
                <li v-for="item in filteredData.itinerary" :key="item.name">
                    <p class="itinerary-name">{{ item.name }}</p>
                    <p>{{ item.description }}</p>
                </li>
            </ul>
        </div>
    </div>
</template>
<style scoped>
.planner {
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
    align-items: center;
    display: flex;
    gap: 8px;

}

.img-update {
    width: 24px;
    background-color: #6D695E;
    border-radius: 8px;
    padding: 6px;
}

h5 {
    color: #6D695E;
    margin: 0;
    font-size: 14px;
}

p {
    color: #CECECE;
    font-size: 14px;
    font-family: 'inter', sans-serif;
}

li {
    border-bottom: 1px dashed #6D695E;
}

ul {
    padding: 0px 16px;
    list-style-type: decimal;
    color: #6D695E;
    font-size: 25px;
    font-family: 'lora', sans-serif;
    font-weight: 100;
    margin-left: 20px;
}

.itinerary-name {
    font-family: 'lora', sans-serif;
    font-weight: 600;
    color: white;
    font-size: 16px;
    margin: 0;
}
</style>