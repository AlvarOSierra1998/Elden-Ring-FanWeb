
<template>
    <nav class="lore">
        <div>
            
            <img  src="../assets/goldenorderlogo.png" alt="golden-order-logo">
            <a href="#lore">
                <button>
                    <h2>Lore</h2>
                </button>
            </a>

            <a href="#lore">
                <button>
                    <h2>New Boss</h2>
                </button>
            </a>


        </div>
    </nav>
</template>

<script setup>
import { ref } from 'vue'



</script>

<style scoped>

.lore {
    background-image: url("../assets/eldenskull.webp");
    height: 1300px;
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5));
    transition: opacity 1s ease-in-out;
    position: relative;

}

.lore::before {
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    height: 50px;
    /* Ajusta esto para cambiar la altura del difuminado */
    background: linear-gradient(to bottom, black, transparent);
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
    width: 20%;
    margin: auto;

}
</style>
