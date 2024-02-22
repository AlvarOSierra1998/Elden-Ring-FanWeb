
<template>
    <div class="lore">
        <div>
            <h1>Lore</h1>
            <p>Some lore about Elden Ring</p>
            <img src="../assets/eldenringlore.webp" alt="Elden Ring Lore">
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'



</script>

<style scoped>
    .lore {
        background-image: url("../assets/ER-SOTE-transformed.webp");
        height: 1300px;
        background-attachment: fixed;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));
        transition: opacity 1s ease-in-out;

    }

    .lore div {
        padding: 5rem;
        text-align: center;
        font-size: 20px;
        color: white;
        margin: auto;
        display: inline-flex;

    }

    .lore img {
        transition: transform 0.5s;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 50%;
        margin: auto;

    }

</style>
