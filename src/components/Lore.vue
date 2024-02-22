
<template>
    <nav class="lore">
        <div class="buttons-container">
            <img  src="../assets/goldenorderlogo.png" alt="golden-order-logo">
            <a href="#lore">
                <button>
                    <h2>Lore</h2>
                </button>
            </a>

            <a href="#boss">
                <button>
                    <h2>New Boss</h2>
                </button>
            </a>

            <a href="#gp">
                <button>
                    <h2>Gameplay</h2>
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
a{
    text-decoration: none;
}
.buttons-container{
    display: flex;
    justify-content: space-around;
    align-items: center;
    margin-top: 10rem;
}
button{
    background: none;
    outline: none;
    border: none;
    color: #ffbf00;
    cursor: pointer;
    font-family: "Quicksand", sans-serif;
    font-optical-sizing: auto;
    font-weight: lighter;
    font-style: normal;
    
}
</style>
