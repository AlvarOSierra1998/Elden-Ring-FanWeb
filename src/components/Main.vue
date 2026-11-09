<template>
  <div
    id="app"
    class="wrapper"
    v-cloak
    :class="{
      'is-previous': isPreviousSlide,
      'first-load': isFirstLoad
    }"
    :style="{
      '--wallpaper-image': wallpaper ? `url('${wallpaper}')` : 'none'
    }"
  >
    <!-- ================= SLIDES ================= -->
    <div
      v-for="(slide, index) in slides"
      :key="index"
      class="slide-wrapper"
      :class="{ active: index === currentSlide }"
      :style="{
        zIndex: slides.length - index,
        backgroundImage: getSlideBackground(slide)
      }"
    >
      <div class="slide-inner">
        <!-- TEXTO DE FONDO -->
        <div class="slide-bg-text">
          <p>{{ slide.headlineFirstLine }}</p>
          <p>{{ slide.headlineSecondLine }}</p>
        </div>

        <!-- RECTÁNGULO -->
        <div class="slide-rect-filter">
          <div
            class="slide-rect"
            :style="{ borderImageSource: getSlideRect(slide) }"
          ></div>
        </div>

        <!-- CONTENIDO -->
        <div class="slide-content">
          <h1 class="slide-content-text">
            <p>{{ slide.headlineFirstLine }}</p>
            <p>{{ slide.headlineSecondLine }}</p>
          </h1>

          <a href="#" class="slide-content-cta" @click.prevent="toogle">
            Mostrar
          </a>
        </div>

        <!-- MODAL -->
        <Modal :show="mostrar" :class="{ desc: mostrar }" @close="toogle">
          <!-- SLIDE 0 - DESCRIPCIÓN -->
          <div v-if="currentSlide === 0" class="bloque">
            <img
              :src="goldenOrder"
              class="book animate__animated animate__fadeInLeft"
              alt="Golden Order Principia"
              @click="toggledesc"
            />

            <transition name="fade">
              <div
                v-if="mostrardesc"
                class="card text-bg-dark container-fluid text-center p-0 m-0"
              >
                <img :src="marika" class="card-img img-background" alt="Marika" />

                <div class="card-img-overlay cartas-grid">
                  <div class="card border-0 carta-props col carta-fondo1">
                    <img
                      :src="erdtreeSigil"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Erdtree"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.description }}</p>
                    </div>
                  </div>
                  <!---- parrafos y cartas no usadas
                  <div class="card border-0 carta-props col carta-fondo2">
                    <img
                      :src="messmer"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Messmer"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.parrafo2 }}</p>
                    </div>
                  </div>

                  <div class="card border-0 carta-props col carta-fondo3">
                    <img
                      :src="erdtree"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Erdtree"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.parrafo3 }}</p>
                    </div>
                  </div>-->
                </div>
              </div>
            </transition>
          </div>

          <!-- SLIDE 1 - PERSONAJES -->
          <div v-else-if="currentSlide === 1" class="bloque">
            <img
              :src="goldenOrder"
              class="book animate__animated animate__fadeInLeft"
              alt="Golden Order Principia"
              @click="togglePersonajes"
            />

            <transition name="fade">
              <div
                v-if="mostrarPersonajes"
                class="card text-bg-dark container-fluid text-center p-0 m-0"
              >
                <img :src="marikaFondo" class="card-img img-background" alt="Marika" />

                <div class="card-img-overlay cartas-grid">
                  <div class="card border-0 carta-props col carta-fondo1">
                    <img
                      :src="leda"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Leda"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje1Lore }}</p>
                    </div>
                  </div>

                  <div class="card border-0 carta-props col carta-fondo2">
                    <img
                      :src="miquella"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Miquella"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje2Lore }}</p>
                    </div>
                  </div>

                  <div class="card border-0 carta-props col carta-fondo3">
                    <img
                      :src="ansbach"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Ansbach"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.personaje3Lore }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </transition>
          </div>

          <!-- SLIDE 2 - ENEMIGOS -->
          <div v-else-if="currentSlide === 2" class="bloque">
            <img
              :src="goldenOrder"
              class="book animate__animated animate__fadeInLeft"
              alt="Golden Order Principia"
              @click="toggleEnemigos"
            />

            <transition name="fade">
              <div
                v-if="mostrarEnemigos"
                class="card text-bg-dark container-fluid text-center p-0 m-0"
              >
                <img :src="marika" class="card-img img-background" alt="Marika" />

                <div class="card-img-overlay cartas-grid">
                  <div class="card border-0 carta-props col carta-fondo1">
                    <img
                      :src="enemigo1"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Enemigo 1"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo1 }}</p>
                    </div>
                  </div>

                  <div class="card border-0 carta-props col carta-fondo2">
                    <img
                      :src="enemigo2"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Enemigo 2"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo2 }}</p>
                    </div>
                  </div>

                  <div class="card border-0 carta-props col carta-fondo3">
                    <img
                      :src="enemigo3"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Enemigo 3"
                    />
                    <div class="card-body">
                      <p class="txt-lore card-text">{{ slide.enemigo3 }}</p>
                    </div>
                  </div>
                </div>
              </div>
            </transition>
          </div>
        </Modal>

        <!-- MENÚ LATERAL -->
        <h2 class="slide-side-text">
          <span>{{ slide.sublineFirstLine }} / </span>
          <span>{{ slide.sublineSecondLine }}</span>
        </h2>
      </div>
    </div>

    <!-- CONTROLES -->
    <div class="controls-container">
      <button
        v-for="(slide, index) in slides"
        :key="index"
        class="controls-button"
        :class="{ active: index === currentSlide }"
        type="button"
        @click="updateSlide(index)"
      >
        {{ slide.headlineFirstLine }}
        {{ slide.headlineSecondLine }}
      </button>
    </div>

    <!-- PAGINACIÓN -->
    <div class="pagination-container">
      <span
        v-for="(slide, index) in slides"
        :key="index"
        class="pagination-item"
        :class="{ active: index === currentSlide }"
        @click="updateSlide(index)"
      ></span>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Modal from './Modal.vue'

/* ============================================================
   ASSETS
   ============================================================ */

const assetFiles = import.meta.glob(
  '../assets/**/*.{png,webp,jpg,jpeg,svg,gif,avif}',
  {
    eager: true,
    import: 'default',
    query: '?url'
  }
)

const normalizeAssetName = (value) => {
  if (!value) return ''
  return String(value)
    .split('/')
    .pop()
    .split('\\')
    .pop()
    .trim()
    .toLowerCase()
}

const findAsset = (fileName) => {
  if (!fileName) return ''
  const normalizedTarget = normalizeAssetName(fileName)

  for (const [path, url] of Object.entries(assetFiles)) {
    if (normalizeAssetName(path) === normalizedTarget) {
      return url
    }
  }
  return ''
}

const getAsset = (fileName) => {
  const asset = findAsset(fileName)
  if (asset) return asset
  if (typeof fileName === 'string' && fileName.startsWith('/')) {
    return fileName
  }
  return ''
}

/* ============================================================
   IMÁGENES FIJAS
   ============================================================ */

const goldenOrder = getAsset('ER_Icon_Book_Golden_Order_Principia.webp')
const marika = getAsset('marika.webp')
const marikaFondo = getAsset('marika-fondo.webp')
const erdtree = getAsset('erdtree.webp')
const ansbach = getAsset('ansbach.avif')
const messmer = getAsset('messmer.webp')
const miquella = getAsset('miquella.webp')
const leda = getAsset('leda.avif')
const erdtreeSigil = getAsset('ER_Spell_Sigil_Erdtree.webp')
const enemigo1 = getAsset('enemigo1.png')
const enemigo2 = getAsset('enemigo2.png')
const enemigo3 = getAsset('enemigo3.png')
const wallpaper = getAsset('wallpaper.jpeg')

/* ============================================================
   COMPROBACIÓN DE ASSETS
   ============================================================ */

const checkAsset = (name, value) => {
  if (!value) {
    console.warn(`[Main.vue] No se encontró el asset: ${name}`)
  }
}

checkAsset('ER_Icon_Book_Golden_Order_Principia.webp', goldenOrder)
checkAsset('marika.webp', marika)
checkAsset('marika-fondo.webp', marikaFondo)
checkAsset('erdtree.webp', erdtree)
checkAsset('ansbach.avif', ansbach)
checkAsset('messmer.webp', messmer)
checkAsset('miquella.webp', miquella)
checkAsset('leda.avif', leda)
checkAsset('ER_Spell_Sigil_Erdtree.webp', erdtreeSigil)
checkAsset('enemigo1.png', enemigo1)
checkAsset('enemigo2.png', enemigo2)
checkAsset('enemigo3.png', enemigo3)
checkAsset('wallpaper.jpeg', wallpaper)

/* ============================================================
   ESTADO
   ============================================================ */

const currentSlide = ref(0)
const isPreviousSlide = ref(false)
const isFirstLoad = ref(true)
const slides = ref([])

const mostrar = ref(false)
const toogle = () => {
  mostrar.value = !mostrar.value
}

const mostrardesc = ref(false)
const toggledesc = () => {
  mostrardesc.value = !mostrardesc.value
}

const mostrarPersonajes = ref(false)
const togglePersonajes = () => {
  mostrarPersonajes.value = !mostrarPersonajes.value
}

const mostrarEnemigos = ref(false)
const toggleEnemigos = () => {
  mostrarEnemigos.value = !mostrarEnemigos.value
}

/* ============================================================
   ASSETS DE LOS SLIDES
   ============================================================ */

const resolveSlideAsset = (value) => {
  if (!value) return ''
  const resolved = getAsset(value)
  if (resolved) return resolved
  return String(value)
}

const getSlideBackground = (slide) => {
  const image = resolveSlideAsset(slide?.bgImg)
  return image ? `url("${image}")` : 'none'
}

const getSlideRect = (slide) => {
  const image = resolveSlideAsset(slide?.rectImg)
  return image ? `url("${image}")` : 'none'
}

/* ============================================================
   CAMBIO DE SLIDE
   ============================================================ */

const updateSlide = (index) => {
  isPreviousSlide.value = index < currentSlide.value
  currentSlide.value = index
  isFirstLoad.value = false

  mostrar.value = false
  mostrardesc.value = false
  mostrarPersonajes.value = false
  mostrarEnemigos.value = false
}

/* ============================================================
   JSON
   ============================================================ */

const fetchSlides = async () => {
  try {
    const response = await fetch('/data.json')

    if (!response.ok) {
      throw new Error(`Error HTTP ${response.status} al cargar data.json`)
    }

    const data = await response.json()

    if (!Array.isArray(data)) {
      throw new Error('data.json debe contener un array de slides')
    }

    slides.value = data
  } catch (error) {
    console.error('[Main.vue] Error cargando data.json:', error)
    slides.value = []
  }
}

/* ============================================================
   TOUCH / SWIPE
   ============================================================ */

let startX = 0
let endX = 0
let productRotatorSlide = null

const handleTouchStart = (event) => {
  startX = event.touches?.[0]?.pageX ?? 0
  endX = startX
}

const handleTouchMove = (event) => {
  endX = event.touches?.[0]?.pageX ?? endX
}

const handleTouchEnd = () => {
  const threshold = startX - endX

  if (threshold > 150 && currentSlide.value < slides.value.length - 1) {
    updateSlide(currentSlide.value + 1)
  }

  if (threshold < -150 && currentSlide.value > 0) {
    updateSlide(currentSlide.value - 1)
  }

  startX = 0
  endX = 0
}

onMounted(() => {
  fetchSlides()

  productRotatorSlide = document.getElementById('app')
  if (!productRotatorSlide) return

  productRotatorSlide.addEventListener('touchstart', handleTouchStart, { passive: true })
  productRotatorSlide.addEventListener('touchmove', handleTouchMove, { passive: true })
  productRotatorSlide.addEventListener('touchend', handleTouchEnd, { passive: true })
})

onUnmounted(() => {
  if (!productRotatorSlide) return

  productRotatorSlide.removeEventListener('touchstart', handleTouchStart)
  productRotatorSlide.removeEventListener('touchmove', handleTouchMove)
  productRotatorSlide.removeEventListener('touchend', handleTouchEnd)

  productRotatorSlide = null
})
</script>

<!-- ============================================================
     VARIABLES RESPONSIVE (sin scoped, en :root)
     ============================================================ -->
<style>
:root {
  /* Modal / cartas */
  --book-width: 300px;
  --card-max: 22rem;         /* ancho máximo de cada carta */
  --cards-gap: 1.25rem;
  --cards-pad: 2rem 1.5rem;
  --lore-size: 1rem;
  --foto-max: 220px;         /* tamaño máx. de la imagen circular de cada carta */

  /* Difuminado de la imagen de fondo (zona roja) */
  --fade-size: 22%;

  /* Slide en móvil (solo ≤767.98px) */
  --rect-left: 12vw;
  --rect-w: 44vw;
  --rect-h: 32vh;
  --rect-border: 3vh;
  --title-size: clamp(2.4rem, 11vw, 4rem);
}

@media (max-width: 1199.98px) {
  :root {
    --book-width: 250px;
    --card-max: 19rem;
    --cards-gap: 1rem;
    --cards-pad: 1.5rem 1rem;
    --lore-size: 0.95rem;
    --foto-max: 180px;
  }
}

@media (max-width: 991.98px) {
  :root {
    --book-width: 200px;
    --card-max: 16rem;
    --cards-gap: 0.75rem;
    --cards-pad: 1.25rem 0.75rem;
    --lore-size: 0.88rem;
    --foto-max: 140px;
    --fade-size: 18%;
  }
}

/* Móvil: una carta por fila (lo decide flex-wrap) */
@media (max-width: 767.98px) {
  :root {
    --book-width: 160px;
    --card-max: 26rem;
    --cards-gap: 1rem;
    --cards-pad: 1.25rem 1rem 2rem;
    --lore-size: 0.9rem;
    --foto-max: 130px;
    --fade-size: 12%;
  }
}

@media (max-width: 479.98px) {
  :root {
    --book-width: 130px;
    --card-max: 100%;
    --lore-size: 0.85rem;
    --foto-max: 110px;
    --rect-w: 46vw;
  }
}
</style>

<style scoped>
@import url("./StyleComponents/loreDesc.css");

/* ============================================================
   TRANSICIONES
   ============================================================ */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* ============================================================
   LIBRO
   ============================================================ */
.book {
  width: var(--book-width);
  max-width: 100%;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: 0.5s !important;
}

/* ============================================================
   MODAL (.desc): el scroll lo gestiona el propio modal
   ============================================================ */
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
  display: inline-flex;
  justify-content: space-evenly;
  background-image: var(--wallpaper-image);
  border-image: fill 0 linear-gradient(
    to top,
    rgba(0, 0, 0, 0.747),
    rgba(0, 0, 0, 0.5)
  );
  background-size: cover;

  max-height: 100dvh;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
}

/* ============================================================
   PANEL DE CARTAS: la altura la marca el contenido
   ============================================================ */
.bloque .card.text-bg-dark {
  position: relative;
  width: 100%;
  overflow: hidden;
}

/* Imagen de fondo = fondo real, no da altura */
.img-background {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;

  /* BORDE DIFUMINADO (zona roja): el corte negro -> imagen se funde
     arriba y abajo, sin capas encima */
  -webkit-mask-image: linear-gradient(
    to bottom,
    transparent 0%,
    #000 var(--fade-size),
    #000 calc(100% - var(--fade-size)),
    transparent 100%
  );
          mask-image: linear-gradient(
    to bottom,
    transparent 0%,
    #000 var(--fade-size),
    #000 calc(100% - var(--fade-size)),
    transparent 100%
  );
}

/* Contenedor de las cartas: se adapta solo, sin saltos bruscos */
.cartas-grid {
  position: relative !important;   /* Bootstrap lo pone absolute */
  display: flex;
  flex-wrap: wrap;
  justify-content: center;         /* una carta suelta queda centrada */
  align-items: flex-start;         /* ninguna carta se estira en alto */
  gap: var(--cards-gap);
  width: 100%;
  max-width: 1400px;
  margin: 0 auto;
  padding: var(--cards-pad);
}

/* Cada carta: mínimo 15rem, máximo --card-max */
.card.carta-props {
  flex: 1 1 min(15rem, 100%);
  width: auto !important;
  min-width: 0;
  max-width: var(--card-max) !important;
  margin: 0 !important;
  padding: 0 !important;
}

/* Texto: nunca partir palabras a mitad */
.txt-lore {
  overflow-wrap: normal;
  word-break: normal;
  hyphens: auto;
  text-align: justify;
}

/* Imagen circular de cada carta */
.foto-top,
.foto-top2 {
  max-width: var(--foto-max);
  max-height: var(--foto-max);
  object-fit: contain;
}

/* Difuminado también en el borde superior de las imágenes de las cartas */
.card-img-top {
  -webkit-mask-image: linear-gradient(to bottom, transparent 0%, #000 22%);
          mask-image: linear-gradient(to bottom, transparent 0%, #000 22%);
  width: 100%;
  margin-top: 40px;
  border-radius: 0;
  
}

.txt-lore {
  font-size: var(--lore-size);
  font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  width: 100%;
}

/* ============================================================
   TABLET (≤991.98px): libro encima, panel debajo
   ============================================================ */
@media (max-width: 991.98px) {
  /* El modal ocupa todo el ancho y apila sus hijos */
  .desc {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: flex-start;
    width: 100%;
    max-width: 100vw;
  }

  .bloque {
    display: flex !important;
    flex-direction: column !important;      /* gana al !important de loreDesc.css */
    align-items: stretch;                   /* el panel ocupa todo el ancho */
    width: 100%;
    max-width: 100vw;
    min-width: 0;
  }

  .book {
    align-self: center;
    margin: 1rem auto;
  }

  /* El panel nunca se encoge al contenido */
  .bloque .card.text-bg-dark {
    width: 100%;
    max-width: 100%;
    min-width: min(100vw, 20rem);
    flex: 0 0 auto;
  }
}

/* ============================================================
   MÓVIL (≤767.98px): slide principal
   ============================================================ */
@media (max-width: 767.98px) {
  .wrapper {
    min-height: 32rem;
  }

  .slide-rect {
    left: var(--rect-left);
    width: var(--rect-w);
    height: var(--rect-h);
    border-width: var(--rect-border);
  }

  .slide-side-text {
    left: calc(var(--rect-left) - 2rem);
    top: calc(50% - var(--rect-h) / 2 + var(--rect-border) / 2);
  }

  .slide-content {
    /* left: calc(var(--rect-left) + var(--rect-w) * 0.6); */
    right: 1rem;
    margin-top: 3rem;
  }

  .slide-content-text {
    font-size: var(--title-size);
    margin-bottom: 0;
  }

  .slide-content-text > p:last-child {
    padding-left: 1.5rem;
  }

  /* loreDesc.css lo oculta a ≤630px: se vuelve a mostrar */
  .slide-content-cta {
    display: block;
    margin: 1.75rem 0 0 1.5rem;
    padding: 0.9rem 1.6rem;
    background-color: rgba(255, 255, 255, 0.3);
  }

  /* Paginación de puntos abajo */
  .pagination-container {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 0.75rem;
    top: auto;
    bottom: 1.25rem;
    right: auto;
    left: 50%;
    transform: translateX(-50%);
  }

  .pagination-item {
    width: 24px;
    height: 4px;
    border-radius: 2px;
  }

  .pagination-item + .pagination-item {
    margin-top: 0;
  }

  .pagination-item.active {
    transform: none;
    width: 34px;
  }

  .pagination-item.active:after {
    display: none;
  }
}

@media (max-width: 630px) {
  .wrapper {
    height: 100dvh;
  }
}
</style>