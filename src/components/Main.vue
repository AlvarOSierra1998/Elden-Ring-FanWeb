<template>
  <div id="app" class="wrapper" v-cloak :class="{'is-previous': isPreviousSlide, 'first-load': isFirstLoad}">
    <div class="slide-wrapper" 
         v-for="(slide, index) in slides" 
         :key="index"
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
          <a href="#" @click.prevent="toogle()" class="slide-content-cta">Mostrar</a> 
        </div>
        <!-- Modal -->
        <Modal :show="mostrar" @close="toogle" :class="{ desc: mostrar }">
          <!-- Slide 0: Las tierras de las sombras -->
          <div v-if="currentSlide === 0" class="bloque">
            <img @click="toggledesc" src="../assets/ER_icon_Book_Golden_Order_Principia.webp" class="book animate__animated animate__fadeInLeft" alt="Golden Order Principia">
            <transition name="fade">
              <div class="card text-bg-dark container-fluid text-center p-0 m-0" v-if="mostrardesc">
                <img src="../assets/marika.webp" class="card-img img-background" alt="marika">
                <div class="card-img-overlay row row-cols-7 p-0 m-0">
                  <div class="card border-0 carta-props col carta-fondo1" style="width: 18rem;">
                    <img src="../assets/ER_Spell_Sigil_Erdtree.webp" class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1" alt="Erdtree">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.description }}</p>
                    </div>
                  </div>
                  <div class="card border-0 carta-props col carta-fondo2" style="width: 18rem;">
                    <img src="../assets/messmer.png" class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2" alt="...">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.parrafo2 }}</p>
                    </div>
                  </div>
                  <div class="card border-0 carta-props col carta-fondo3" style="width: 18rem;">
                    <img src="../assets/erdtree.webp" class="card-img-top foto-top animate__animated animate__fadeInDown elemento3" alt="...">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.parrafo3 }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </transition>
          </div>
          <!-- Slide 1: Personajes principales -->
          <div v-else-if="currentSlide === 1" class="bloque">
            <img @click="togglePersonajes" src="../assets/ER_icon_Book_Golden_Order_Principia.webp" class="book animate__animated animate__fadeInLeft" alt="Golden Order Principia">
            <transition name="fade">
              <div class="card text-bg-dark container-fluid text-center p-0 m-0" v-if="mostrarPersonajes">
                <img src="../assets/marika-fondo.webp" class="card-img img-background" alt="marika">
                <div class="card-img-overlay row row-cols-7 p-0 m-0">
                  <div class="card border-0 carta-props col carta-fondo1" style="width: 18rem;">
                    <img src="../assets/ledaFullBody.png" class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1" alt="Leda">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje1Lore }}</p>
                    </div>
                  </div> 
                  <div class="card border-0 carta-props col carta-fondo2" style="width: 18rem;">
                    <img src="../assets/messmer.png" class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2" alt="Messmer">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje2Lore }}</p>
                    </div>
                  </div>
                  <div class="card border-0 carta-props col carta-fondo3" style="width: 18rem;">
                    <img src="../assets/erdtree.webp" class="card-img-top foto-top animate__animated animate__fadeInDown elemento3" alt="Erdtree">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje3Lore }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </transition>
          </div>
          <!-- Slide 2: Enemigos principales -->
          <div v-else-if="currentSlide === 2" class="bloque">
            <img @click="toggleEnemigos" src="../assets/ER_icon_Book_Golden_Order_Principia.webp" class="book animate__animated animate__fadeInLeft" alt="Golden Order Principia">
            <transition name="fade">
              <div class="card text-bg-dark container-fluid text-center p-0 m-0" v-if="mostrarEnemigos">
                <img src="../assets/marika.webp" class="card-img img-background" alt="marika">
                <div class="card-img-overlay row row-cols-7 p-0 m-0">
                  <div class="card border-0 carta-props col carta-fondo1" style="width: 18rem;">
                    <img src="../assets/enemigo1.png" class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1" alt="Enemigo1">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo1 }}</p>
                    </div>
                  </div>
                  <div class="card border-0 carta-props col carta-fondo2" style="width: 18rem;">
                    <img src="../assets/enemigo2.png" class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2" alt="Enemigo2">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo2 }}</p>
                    </div>
                  </div>
                  <div class="card border-0 carta-props col carta-fondo3" style="width: 18rem;">
                    <img src="../assets/enemigo3.png" class="card-img-top foto-top animate__animated animate__fadeInDown elemento3" alt="Enemigo3">
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo3 }}</p>
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
              :key="index"
              :class="{ active: index === currentSlide }"
              @click="updateSlide(index)">
        {{ slide.headlineFirstLine }} {{ slide.headlineSecondLine }}
      </button>
    </div>
    <div class="pagination-container">
      <span class="pagination-item"
            v-for="(slide, index) in slides"
            :key="index"
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
const toggledesc = () =>{
  mostrardesc.value = !mostrardesc.value;
}

const mostrarPersonajes = ref(false);
const togglePersonajes = () => {
  mostrarPersonajes.value = !mostrarPersonajes.value;
}

const mostrarEnemigos = ref(false);
const toggleEnemigos = () => {
  mostrarEnemigos.value = !mostrarEnemigos.value;
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

.tabs {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
}
.tabs button {
  padding: 0.5rem 1rem;
  background: #222;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 0.5rem 0.5rem 0 0;
  font-weight: bold;
}
.tabs button.active {
  background: #ffd700;
  color: #222;
}

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