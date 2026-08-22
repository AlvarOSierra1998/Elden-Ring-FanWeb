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
    <!-- ================================================= -->
    <!-- SLIDES -->
    <!-- ================================================= -->

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

        <!-- ================================================= -->
        <!-- TEXTO DE FONDO -->
        <!-- ================================================= -->

        <div class="slide-bg-text">
          <p>{{ slide.headlineFirstLine }}</p>
          <p>{{ slide.headlineSecondLine }}</p>
        </div>

        <!-- ================================================= -->
        <!-- RECTÁNGULO -->
        <!-- ================================================= -->

        <div class="slide-rect-filter">
          <div
            class="slide-rect"
            :style="{
              borderImageSource: getSlideRect(slide)
            }"
          ></div>
        </div>

        <!-- ================================================= -->
        <!-- CONTENIDO -->
        <!-- ================================================= -->

        <div class="slide-content">
          <h1 class="slide-content-text">
            <p>{{ slide.headlineFirstLine }}</p>
            <p>{{ slide.headlineSecondLine }}</p>
          </h1>

          <a
            href="#"
            class="slide-content-cta"
            @click.prevent="toogle"
          >
            Mostrar
          </a>
        </div>

        <!-- ================================================= -->
        <!-- MODAL -->
        <!-- ================================================= -->

        <Modal
          :show="mostrar"
          :class="{ desc: mostrar }"
          @close="toogle"
        >

          <!-- ================================================= -->
          <!-- SLIDE 0 - DESCRIPCIÓN -->
          <!-- ================================================= -->

          <div
            v-if="currentSlide === 0"
            class="bloque"
          >
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
                <img
                  :src="marika"
                  class="card-img img-background"
                  alt="Marika"
                />

                <div
                  class="card-img-overlay row row-cols-7 p-0 m-0"
                >

                  <!-- CARTA 1 -->
                  <div
                    class="card border-0 carta-props col carta-fondo1"
                    style="width: 18rem;"
                  >
                    <img
                      :src="erdtreeSigil"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Erdtree"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.description }}
                      </p>
                    </div>
                  </div>

                  <!-- CARTA 2 -->
                  <div
                    class="card border-0 carta-props col carta-fondo2"
                    style="width: 18rem;"
                  >
                    <img
                      :src="messmer"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Messmer"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.parrafo2 }}
                      </p>
                    </div>
                  </div>

                  <!-- CARTA 3 -->
                  <div
                    class="card border-0 carta-props col carta-fondo3"
                    style="width: 18rem;"
                  >
                    <img
                      :src="erdtree"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Erdtree"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.parrafo3 }}
                      </p>
                    </div>
                  </div>

                </div>
              </div>
            </transition>
          </div>

          <!-- ================================================= -->
          <!-- SLIDE 1 - PERSONAJES -->
          <!-- ================================================= -->

          <div
            v-else-if="currentSlide === 1"
            class="bloque"
          >
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
                <img
                  :src="marikaFondo"
                  class="card-img img-background"
                  alt="Marika"
                />

                <div
                  class="card-img-overlay row row-cols-7 p-0 m-0"
                >

                  <!-- PERSONAJE 1 -->
                  <div
                    class="card border-0 carta-props col carta-fondo1"
                    style="width: 18rem;"
                  >
                    <img
                      :src="leda"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Leda"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.personaje1Lore }}
                      </p>
                    </div>
                  </div>

                  <!-- PERSONAJE 2 -->
                  <div
                    class="card border-0 carta-props col carta-fondo2"
                    style="width: 18rem;"
                  >
                    <img
                      :src="messmer"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Messmer"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.personaje2Lore }}
                      </p>
                    </div>
                  </div>

                  <!-- PERSONAJE 3 -->
                  <div
                    class="card border-0 carta-props col carta-fondo3"
                    style="width: 18rem;"
                  >
                    <img
                      :src="erdtree"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Erdtree"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.personaje3Lore }}
                      </p>
                    </div>
                  </div>

                </div>
              </div>
            </transition>
          </div>

          <!-- ================================================= -->
          <!-- SLIDE 2 - ENEMIGOS -->
          <!-- ================================================= -->

          <div
            v-else-if="currentSlide === 2"
            class="bloque"
          >
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
                <img
                  :src="marika"
                  class="card-img img-background"
                  alt="Marika"
                />

                <div
                  class="card-img-overlay row row-cols-7 p-0 m-0"
                >

                  <!-- ENEMIGO 1 -->
                  <div
                    class="card border-0 carta-props col carta-fondo1"
                    style="width: 18rem;"
                  >
                    <img
                      :src="enemigo1"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento1"
                      alt="Enemigo 1"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.enemigo1 }}
                      </p>
                    </div>
                  </div>

                  <!-- ENEMIGO 2 -->
                  <div
                    class="card border-0 carta-props col carta-fondo2"
                    style="width: 18rem;"
                  >
                    <img
                      :src="enemigo2"
                      class="card-img-top foto-top2 animate__animated animate__fadeInDown elemento2"
                      alt="Enemigo 2"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.enemigo2 }}
                      </p>
                    </div>
                  </div>

                  <!-- ENEMIGO 3 -->
                  <div
                    class="card border-0 carta-props col carta-fondo3"
                    style="width: 18rem;"
                  >
                    <img
                      :src="enemigo3"
                      class="card-img-top p-0 foto-top animate__animated animate__fadeInDown elemento3"
                      alt="Enemigo 3"
                    />

                    <div class="card-body">
                      <p class="txt-lore card-text">
                        {{ slide.enemigo3 }}
                      </p>
                    </div>
                  </div>

                </div>
              </div>
            </transition>
          </div>

        </Modal>

        <!-- ================================================= -->
        <!-- MENÚ LATERAL -->
        <!-- ================================================= -->

        <h2 class="slide-side-text">
          <span>{{ slide.sublineFirstLine }} / </span>
          <span>{{ slide.sublineSecondLine }}</span>
        </h2>

      </div>
    </div>

    <!-- ================================================= -->
    <!-- CONTROLES -->
    <!-- ================================================= -->

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

    <!-- ================================================= -->
    <!-- PAGINACIÓN -->
    <!-- ================================================= -->

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

/*
 * IMPORTANTE:
 *
 * En vez de hacer:
 *
 * import marika from '../assets/marika.webp'
 *
 * usamos import.meta.glob().
 *
 * De esta manera Vite obtiene todos los archivos reales que
 * existen en src/assets y podemos buscarlos ignorando
 * mayúsculas/minúsculas.
 */

const assetFiles = import.meta.glob(
  '../assets/**/*.{png,webp,jpg,jpeg,svg,gif}',
  {
    eager: true,
    import: 'default',
    query: '?url'
  }
)

/*
 * Normaliza un nombre de archivo.
 *
 * Ejemplo:
 *
 * Marika.webp
 * MARIKA.WEBP
 * marika.webp
 *
 * terminan siendo comparables.
 */
const normalizeAssetName = (value) => {
  if (!value) {
    return ''
  }

  return String(value)
    .split('/')
    .pop()
    .split('\\')
    .pop()
    .trim()
    .toLowerCase()
}

/*
 * Busca un asset dentro de src/assets.
 *
 * Si data.json contiene:
 *
 * /assets/fondo.webp
 *
 * también intentará localizar:
 *
 * src/assets/fondo.webp
 *
 * aunque el nombre real tenga diferencias de mayúsculas.
 */
const findAsset = (fileName) => {
  if (!fileName) {
    return ''
  }

  const normalizedTarget = normalizeAssetName(fileName)

  for (const [path, url] of Object.entries(assetFiles)) {
    const normalizedPath = normalizeAssetName(path)

    if (normalizedPath === normalizedTarget) {
      return url
    }
  }

  return ''
}

/*
 * Obtiene un asset de forma segura.
 *
 * Si no está en src/assets pero la ruta empieza por /,
 * devuelve la ruta original para permitir archivos de public/.
 */
const getAsset = (fileName) => {
  const asset = findAsset(fileName)

  if (asset) {
    return asset
  }

  if (typeof fileName === 'string' && fileName.startsWith('/')) {
    return fileName
  }

  return ''
}

/* ============================================================
   IMÁGENES FIJAS
   ============================================================ */

const goldenOrder = getAsset(
  'ER_Icon_Book_Golden_Order_Principia.webp'
)

const marika = getAsset(
  'marika.webp'
)

const marikaFondo = getAsset(
  'marika-fondo.webp'
)

const erdtree = getAsset(
  'erdtree.webp'
)

const messmer = getAsset(
  'messmer.png'
)

const leda = getAsset(
  'LedaFullBody.png'
)

const erdtreeSigil = getAsset(
  'ER_Spell_Sigil_Erdtree.webp'
)

const enemigo1 = getAsset(
  'enemigo1.png'
)

const enemigo2 = getAsset(
  'enemigo2.png'
)

const enemigo3 = getAsset(
  'enemigo3.png'
)

const wallpaper = getAsset(
  'wallpaper.jpeg'
)

/* ============================================================
   COMPROBACIÓN DE ASSETS
   ============================================================ */

const checkAsset = (name, value) => {
  if (!value) {
    console.warn(
      `[Main.vue] No se encontró el asset: ${name}`
    )
  }
}

checkAsset('ER_Icon_Book_Golden_Order_Principia.webp', goldenOrder)
checkAsset('marika.webp', marika)
checkAsset('marika-fondo.webp', marikaFondo)
checkAsset('erdtree.webp', erdtree)
checkAsset('messmer.png', messmer)
checkAsset('LedaFullBody.png', leda)
checkAsset('ER_Spell_Sigil_Erdtree.webp', erdtreeSigil)
checkAsset('enemigo1.png', enemigo1)
checkAsset('enemigo2.png', enemigo2)
checkAsset('enemigo3.png', enemigo3)
checkAsset('wallpaper.jpeg', wallpaper)

/* ============================================================
   SLIDES
   ============================================================ */

const currentSlide = ref(0)
const isPreviousSlide = ref(false)
const isFirstLoad = ref(true)
const slides = ref([])

/* ============================================================
   MODAL PRINCIPAL
   ============================================================ */

const mostrar = ref(false)

const toogle = () => {
  mostrar.value = !mostrar.value
}

/* ============================================================
   DESCRIPCIÓN
   ============================================================ */

const mostrardesc = ref(false)

const toggledesc = () => {
  mostrardesc.value = !mostrardesc.value
}

/* ============================================================
   PERSONAJES
   ============================================================ */

const mostrarPersonajes = ref(false)

const togglePersonajes = () => {
  mostrarPersonajes.value = !mostrarPersonajes.value
}

/* ============================================================
   ENEMIGOS
   ============================================================ */

const mostrarEnemigos = ref(false)

const toggleEnemigos = () => {
  mostrarEnemigos.value = !mostrarEnemigos.value
}

/* ============================================================
   ASSETS DE LOS SLIDES
   ============================================================ */

/*
 * Convierte una imagen procedente de data.json en una URL
 * que Vite pueda utilizar.
 *
 * Por ejemplo:
 *
 * slide.bgImg = "/assets/background.webp"
 *
 * buscará background.webp dentro de src/assets.
 */
const resolveSlideAsset = (value) => {
  if (!value) {
    return ''
  }

  const resolved = getAsset(value)

  if (resolved) {
    return resolved
  }

  return String(value)
}

/* ============================================================
   BACKGROUND DE CADA SLIDE
   ============================================================ */

const getSlideBackground = (slide) => {
  const image = resolveSlideAsset(slide?.bgImg)

  if (!image) {
    return 'none'
  }

  return `url("${image}")`
}

/* ============================================================
   RECTÁNGULO DE CADA SLIDE
   ============================================================ */

const getSlideRect = (slide) => {
  const image = resolveSlideAsset(slide?.rectImg)

  if (!image) {
    return 'none'
  }

  return `url("${image}")`
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
      throw new Error(
        `Error HTTP ${response.status} al cargar data.json`
      )
    }

    const data = await response.json()

    if (!Array.isArray(data)) {
      throw new Error(
        'data.json debe contener un array de slides'
      )
    }

    slides.value = data
  } catch (error) {
    console.error(
      '[Main.vue] Error cargando data.json:',
      error
    )

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

  /*
   * SWIPE HACIA LA IZQUIERDA
   */
  if (
    threshold > 150 &&
    currentSlide.value < slides.value.length - 1
  ) {
    updateSlide(currentSlide.value + 1)
  }

  /*
   * SWIPE HACIA LA DERECHA
   */
  if (
    threshold < -150 &&
    currentSlide.value > 0
  ) {
    updateSlide(currentSlide.value - 1)
  }

  startX = 0
  endX = 0
}

/* ============================================================
   MOUNT
   ============================================================ */

onMounted(() => {
  fetchSlides()

  productRotatorSlide =
    document.getElementById('app')

  if (!productRotatorSlide) {
    return
  }

  productRotatorSlide.addEventListener(
    'touchstart',
    handleTouchStart,
    { passive: true }
  )

  productRotatorSlide.addEventListener(
    'touchmove',
    handleTouchMove,
    { passive: true }
  )

  productRotatorSlide.addEventListener(
    'touchend',
    handleTouchEnd,
    { passive: true }
  )
})

/* ============================================================
   UNMOUNT
   ============================================================ */

onUnmounted(() => {
  if (!productRotatorSlide) {
    return
  }

  productRotatorSlide.removeEventListener(
    'touchstart',
    handleTouchStart
  )

  productRotatorSlide.removeEventListener(
    'touchmove',
    handleTouchMove
  )

  productRotatorSlide.removeEventListener(
    'touchend',
    handleTouchEnd
  )

  productRotatorSlide = null
})
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

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.book {
  width: 300px;
  top: 0;
  left: 0;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: 0.5s !important;
}

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
}
</style>