<script setup>
import { ref, onMounted } from 'vue';
import vector from '@/assets/icons/Vector.svg';
import { useRouter } from 'vue-router';

const baseURL = import.meta.env.VITE_APP_BASE_URL;
const router = useRouter();
const data = ref(null);

onMounted(async () => {
    try {
        const response = await fetch(`${baseURL}/v1/planners`);
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        data.value = await response.json();
    } catch (error) {
        console.error(error);
    }
    console.log(data.value);
});

function redirectToPlanner(plannerId) {
    router.push(`/planner/${plannerId}`);
}
</script>

<template>
    <div>
        <h4>Derniers itinéraires</h4>
        <div class="list-history" v-for="(item) in data" @click="redirectToPlanner(item.id)">
            <p>{{ item.prompt }}</p>
            <img :src="vector" alt="icon-voir-pls" />
        </div>
    </div>
</template>

<style scoped>
.list-history {
    background-color: #242321;
    border: 1px solid #6D695E;
    border-radius: 8px;
    width: 85vw;
    padding:  8px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 8px;
}

p {
    margin: 4px;
}

h4 {
    color: #6D695E;
}
</style>