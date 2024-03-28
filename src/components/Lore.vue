
<template>
    <nav class="lore">
        <img  src="../assets/goldenorderlogo.png" alt="golden-order-logo">
        <div class="container">
            
            <div class="buttons-container">
                <button @click="mostrarLoreDesc"><a href="#lore">Lore</a></button>
                <button><a href="#characters">Characters</a></button>
                <button><a href="#gameplay">trailer</a></button>
                <button><a href="#gallery">Gallery</a></button>
            </div>
        </div>
    </nav>
    <!--LORE-->
    <section>
        <div class="container-dsc" v-if="mostrarLore":class = "{desc:mostrarLoreDesc}" >
        <div class="desc" >
            <h1>ELDEN RING</h1>
            <p id="lore">Un juego de rol de acción en tercera persona de mundo abierto desarrollado por FromSoftware y publicado por Bandai Namco Entertainment. Fue lanzado el 25 de febrero de 2022 para Microsoft Windows, PlayStation 4, PlayStation 5, Xbox One y Xbox Series X/S.</p>
        </div>
    </div>
    </section>


    
</template>

<script setup>
import { ref } from 'vue';


//Mostrar Lore
const mostrarLore = ref(false);
const mostrarLoreDesc = () =>{
    mostrarLore.value = !mostrarLore.value;

}





</script>

<style scoped>


.container-dsc{
    margin: auto;
}
.desc{
    font-size: 1.5rem;
    font-family: 'Roboto', sans-serif;
    color: #f5f5f5;
    margin: auto;
    padding: 0;
    text-align: justify;
    text-justify: inter-word;
    line-height: 1.5;
    margin-top: 1rem;
    margin-bottom: 1rem;
    width: 60%;
    /*REVISAR*/
    display: inline-flex;
    justify-content: space-evenly ;
}

.lore {
    margin: 5%;
    margin: auto;
    text-align: center;
    background-image: url("../assets/eldenskull.webp");
    height: 600px;
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.493), rgba(0, 0, 0, 0.5));
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
.lore::after{
    content: "";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 50px; /* Ajusta esto para cambiar la altura del difuminado */
    background: linear-gradient(to top, black, transparent);

}


.lore div {
    padding: 5rem;
    text-align: center;
    font-size: 20px;
    color: white;
    margin: auto;
    display: flex;

}

img {
    transition: transform 0.5s;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 10%;
    margin: auto;

}
a{
    text-decoration: none;
    color: #ffbf00;
    transition: 0.5s;
}
.container{
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
    font-size: 1.20em;

    
}
a:hover{
    background-color: rgb(32, 32, 32);
    padding: 1em;
    border-radius: 10px;
    transition: 0.5s;
    color: aliceblue;

}
.buttons-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 50%;
    margin: auto;
    
}
</style>
