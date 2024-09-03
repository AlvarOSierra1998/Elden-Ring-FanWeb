<template>
<nav class="lore">

    <div class="box-button box-button-npcs">
                <button @click="mostrarLorePersonajes"><a href="#characters">Characters</a></button>
    </div>

</nav>


  <!---PERSONAJES -->
  <div v-if="mostrarPersonajes" :class="{ desc: mostrarLorePersonajes }">
            <div>
                <button> Dioses /</button>
                <button id="characters"  class="btn-semi" @click="mostrarDescSemidioses"><a href="#Semidioses"> Semidioses </a>  / </button>
                <button >Npcs </button>
            </div>
    </div>

    <!---NPCS  -->
   
    <section class="color">
            <div>
                <div class="container-dsc" v-if="semidioses" :class="{ desc: mostrarDescSemidioses }">

                    <div class="desc">
                        <img class="book" src="../assets/Mohg.webp" alt="">

                        <p class="lore-desc" id="Semidioses">Mohg, el Señor de la Sangre, era el hermano gemelo de Morgott,
                            ambos nacidos del Linaje
                            Dorado y malditos como Augurios. Mientras que Morgott rechazó su maldición, Mohg la abrazó y
                            en
                            las profundidades subterráneas se conectó con la Madre Informe, un dios exterior que le
                            otorgó
                            poderosas habilidades de hemofuego. Tras la destrucción del Círculo de Elden, Mohg escapó y
                            reclamó un fragmento del Círculo roto, asumiendo el título de Señor de la Sangre y
                            comenzando a
                            reunir seguidores en su guarida subterránea.
                            <br>
                            <br>
                            Mohg desarrolló una obsesión con Miquella el Inmaculado, un Empíreo con el potencial de
                            convertirse en divinidad. Secuestró a Miquella de su Árbol Hierático, con la intención de
                            elevarlo a la divinidad y gobernar juntos como monarcas. Desde su Palacio de Mohgwyn, Mohg
                            estableció su dinastía, servido por nobles y seguidores que ofrecían sangre para despertar a
                            Miquella, aunque nunca logró obtener una respuesta del joven Empíreo.
                            <br>
                            <br>
                            Eventualmente, el Sinluz encontró el palacio de Mohg y lo enfrentó en combate. A pesar de
                            desatar todo el poder de su sangre maldita, Mohg fue derrotado. Tras su muerte, Miquella
                            intentó
                            usar el cuerpo de Mohg como recipiente para el alma del General Radahn, pero ambos fueron
                            derrotados por el Sinluz, y el cuerpo de Mohg fue destruido, sin dejar rastro.

                        </p>
                    </div>
                </div>
            </div>

        </section>
</template>

<script setup>

//Mostrar Lore Personajes botones
const mostrarPersonajes = ref(false);
const mostrarLorePersonajes = () => {
    mostrarPersonajes.value = !mostrarPersonajes.value;
}


const semidioses = ref(false);
const mostrarDescSemidioses = () => {
    semidioses.value = !semidioses.value;
}

</script>