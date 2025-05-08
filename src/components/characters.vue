<!---<template>
<nav class="lore">

    <div class="box-button box-button-npcs">
                <button @click="mostrarLorePersonajes"><a href="#characters">Characters</a></button>
    </div>

</nav>


  <!---PERSONAJES --
  <div v-if="mostrarPersonajes" :class="{ desc: mostrarLorePersonajes }">
            <div>
                <button> Dioses /</button>
                <button id="characters"  class="btn-semi" @click="mostrarDescSemidioses"><a href="#Semidioses"> Semidioses </a>  / </button>
                <button >Npcs </button>
            </div>
    </div>

    <!---NPCS  --
   
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
</template>-->

<!---><script setup>

//Mostrar Lore Personajes botones
const mostrarPersonajes = ref(false);
const mostrarLorePersonajes = () => {
    mostrarPersonajes.value = !mostrarPersonajes.value;
}


const semidioses = ref(false);
const mostrarDescSemidioses = () => {
    semidioses.value = !semidioses.value;
}

</script>-->


    <template>
  <div id="app" class="wrapper" v-cloak :class="{'is-previous': isPreviousSlide, 'first-load': isFirstLoad}">
    <div class="slide-wrapper" 
         v-for="(slide, index) in slides" 
         :class="{ active: index === currentSlide }"
         :style="{ 'z-index': (slides.length - index), 'background-image': 'url(' + slide.bgImg + ')' }">
      <div class="slide-inner">
        <div class="slide-bg-text">
          <p>{{ slide.headlineFirstLine }}</p>
          <p>{{ slide.headlineSecondLine }}</p>
        </div>
        <div class="slide-rect-filter">
          <div class="slide-rect" :style="{'border-image-source': 'url(' + slide.rectImg + ')'}"></div>
        </div>
        <div class="slide-content">
          <h1 class="slide-content-text">
            <p>{{ slide.headlineFirstLine }}</p>
            <p>{{ slide.headlineSecondLine }}</p>
          </h1>
          <!--CALL TO ACTION-->
          <a href="lore" @click.prevent="toogle()" class="slide-content-cta">Mostrar</a> 
        </div>
        <!--modal-->
              <Modal :show="mostrar" @close="toogle" :class="{ desc: mostrar }"  >
              
                <div class="bloque">
                  
                  <img @click="toggledesc"  src="../assets/ER_icon_Book_Golden_Order_Principia.webp" class="book animate__animated animate__fadeInLeft" alt="Golden Order Principia">
                  <transition name="fade">

                    <div class="card text-bg-dark  container-fluid text-center p-0 m-0" v-if="mostrardesc">
                      <img src="../assets/marika.webp" class="card-img img-background" alt="marika">
                      <div class="card-img-overlay row row-cols-7 p-0 m-0 " v-if="slides.length > 0">
                      

                      <div class="card border-0 carta-props col carta-fondo1" style="width: 18rem;">
                          <img src="../assets/ER_Spell_Sigil_Erdtree.webp" class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1" alt="Erdtree">
                        <div class="card-body">
                          <p class=" txt-lore card-text">{{ slides[currentSlide].description }}</p>
                        
                        </div>
                      </div>
                      <div class="card border-0 carta-props col carta-fondo2 " style="width: 18rem;">
                          <img src="../assets/messmer.png" class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2" alt="...">
                        <div class="card-body">
                          <p class=" txt-lore card-text">{{ slides[currentSlide].parrafo2 }}</p>
                        </div>
                      </div>

                      <div class="card border-0 carta-props  col carta-fondo3" style="width: 18rem;">
                          <img src="../assets/erdtree.webp" class="card-img-top foto-top animate__animated animate__fadeInDown elemento3" alt="...">
                        <div class="card-body ">
                          <p class=" txt-lore card-text">{{ slides[currentSlide].parrafo3 }}</p>
                        </div>
                      </div>
                      
                    </div>
                  </div>
                </transition>

                </div>
               
                 
                </Modal>

        <!--MENU SLIDES-->
        <h2 class="slide-side-text">
          <span>{{ slide.sublineFirstLine }} / </span>
          <span>{{ slide.sublineSecondLine }}</span>
        </h2>
      </div>
    </div>
    <div class="controls-container">
      <button class="controls-button" 
              v-for="(slide, index) in slides"
              :class="{ active: index === currentSlide }"
              @click="updateSlide(index)">
        {{ slide.headlineFirstLine }} {{ slide.headlineSecondLine }}
      </button>
    </div>
    <div class="pagination-container">
      <span class="pagination-item"
            v-for="(slide, index) in slides"
            :class="{ active: index === currentSlide }"
            @click="updateSlide(index)">
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import Modal from './Modal.vue';

const mostrar = ref(false);
const toogle = () => {
    mostrar.value = !mostrar.value;
}
const currentSlide = ref(0);
const isPreviousSlide = ref(false);
const isFirstLoad = ref(true);
const slides = ref([]);

const mostrardesc = ref(false);
// const book = ref(true);
const toggledesc = () =>{
  mostrardesc.value = !mostrardesc.value;
  
}

//funciones que controla los slides
const updateSlide = (index) => {
  isPreviousSlide.value = index < currentSlide.value;
  currentSlide.value = index;
  isFirstLoad.value = false;
  mostrar.value= false; //cerrar modal cuando hago click en otro slide
};

onMounted(() => {
    fetchSlides()
  const productRotatorSlide = document.getElementById("app");
  let startX = 0;
  let endX = 0;

  productRotatorSlide.addEventListener("touchstart", (event) => startX = event.touches[0].pageX);

  productRotatorSlide.addEventListener("touchmove", (event) => endX = event.touches[0].pageX);

  productRotatorSlide.addEventListener("touchend", () => {
    const threshold = startX - endX;

    if (threshold < 150 && currentSlide.value > 0) {
      currentSlide.value--;
    }
    if (threshold > -150 && currentSlide.value < slides.value.length - 1) {
      currentSlide.value++;
    }
  });
});

//Peticiones JSON
const fetchSlides = async () => {
  try {
    const response = await fetch('/data.json');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    slides.value = data;
  } catch (error) {
    console.error('Error fetching slides:', error);
  }
};

</script>



<style scoped>
@import url("./StyleComponents/loreDesc.css");



/* Añade tus estilos aquí */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter, .fade-leave-to /* .fade-leave-active en versiones anteriores de Vue */ {
  opacity: 0;
}

.book{
    width: 300px;

    top: 0;
    left: 0;
    margin: auto;
    display: flex ;
    justify-content: center  ;
    align-items: center ;
    cursor: pointer;
    transition: 0.5s !important;

}
/* .book:hover{
   width: 360px;
    transition: 0.5s !important;
} */


.desc {
    font-size: 1rem;
    font-family: 'Roboto', sans-serif;
    color: #f5f5f5;
    margin: auto;
    padding: 0;
    text-align: justify;
    text-justify: inter-word;
    line-height: 1.5;
    
    
    width: 100%;
    /*REVISAR*/
    display: inline-flex;
    justify-content: space-evenly;
    background-image: url("../assets/wallpaper.jpeg");
    border-image: fill 0 linear-gradient(to top, rgba(0, 0, 0, 0.747), rgba(0, 0, 0, 0.5));
    background-size: cover;

}

</style>


