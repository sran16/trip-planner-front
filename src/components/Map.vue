<script setup>
import { ref, onMounted } from 'vue';


let map = ref(null);

onMounted(() => {
    map.value = L.map('map').setView([51.505, -0.09], 13);
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
    }).addTo(map.value);

    L.marker([51.5, -0.09]).addTo(map.value)
        .bindPopup('Marker 1');
    L.marker([51.505, -0.08]).addTo(map.value)
        .bindPopup('Marker 2');
    L.marker([51.51, -0.1]).addTo(map.value)
        .bindPopup('Marker 3');
});
</script>

<template>
    <div id="map" style="height: 400px;"></div>
</template>