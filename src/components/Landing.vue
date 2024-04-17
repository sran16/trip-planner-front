<script setup>
import landing_icon  from "@/assets/icons/Landing_icon.png";
</script>
<template>
    <section>
        <img :src="landing_icon" alt="landing_icon" />
        <h1>Planificateur de voyage</h1>
        <p>généreé par IA</p>
    </section>
</template>
<style scoped>
section {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 10%;
    text-align: center;
    padding: 16px;
    margin-top: 15%;
}
h1 {
    font-family: 'lora', sans-serif;
    font-size: 32px;
    margin: 8px 0;

}
p{
    font-family: 'lora', sans-serif;
    color: #6D695E;
    padding: 0;
    margin: 0;
}
</style>