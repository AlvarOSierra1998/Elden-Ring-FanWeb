<template>
    <div class="parallax" :style="{ opacity: opacityValue }">
        <div>
            <img src="../assets/elden-ring-shadow-of-the-erdtree-logo.png" alt="logo-elden">
        </div>
        
    </div>
</template>

<script setup>


import { ref, onMounted, onBeforeUnmount } from 'vue';

const opacityValue = ref(0);

onMounted(() => {
    window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
    window.removeEventListener('scroll', handleScroll);
});

function handleScroll() {
    opacityValue.value = window.scrollY / 200;
}


</script>
<style scoped >


    .parallax div {
        padding: 5rem;
        text-align: center;
        font-size: 20px;
        color: white;
        margin: auto;
        display: inline-flex;
        overflow: hidden;

    }

    .parallax img {
        transition: transform 0.5s;
        display: flex;
        align-items: center;
        justify-content: center;
        width: 50%;
        margin: auto;
        

    }

    

    .parallax {
        transition: opacity 1s ease-in-out;
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 1300px;
        background-attachment: fixed;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        margin-bottom: 40rem;
        padding-bottom: 10rem;
        background-image: url("../assets/marika.webp");
        border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.719), rgba(0, 0, 0, 0.5));
    }

    .parallax::after {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 50px; /* Ajusta esto para cambiar la altura del difuminado */
    background: linear-gradient(to top, black, transparent);
}
    
</style>