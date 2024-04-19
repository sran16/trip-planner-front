<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

// Define reactive variables

const data = ref(null);
const locations = ref([]);
let map = ref(null);

onMounted(async () => {
    try {
        const route = useRoute();
        const id = route.params.id;

        // Create a Leaflet map and set the initial view
        map.value = L.map('map').setView([51.505, -0.09], 13);

        // Add a tile layer to the map using OpenStreetMap data
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
        }).addTo(map.value);

        // Fetch the planner data from the server
        const response = await fetch(`http://localhost:3000/v1/planners/${id}`);
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const jsonResponse = await response.json();

        // Store the fetched data in reactive variables

        data.value = jsonResponse;
        locations.value = jsonResponse.itinerary;

        // Create markers for each location and add them to the map

        const markers = locations.value.map((location) => {
            return L.marker([
                location.location.latitude,
                location.location.longitude,
            ]).addTo(map.value);
        });

        // Create a feature group from the markers and fit the map bounds to the group

        const group = L.featureGroup(markers);
        map.value.fitBounds(group.getBounds());
    } catch (error) {
        console.error(error);
    }
});
</script>

<template>
    <div id="map"></div>
</template>

<style scoped>
#map {
    height: 50vh;
    width: 100vw;
}
</style>