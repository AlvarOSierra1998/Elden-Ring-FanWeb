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


.parallax {
        background-image: url("../assets/eldenskull.webp");
        height: 1300px;
        background-attachment: fixed;
        background-position: center;
        background-repeat: no-repeat;
        background-size: cover;
        border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));
        transition: opacity 1s ease-in-out;

    }

    .parallax div {
        padding: 5rem;
        text-align: center;
        font-size: 20px;
        color: white;
        margin: auto;
        display: inline-flex;

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
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
</style>