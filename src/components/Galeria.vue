<template>
  <ul class="galeria">
    <li
      v-for="(item, i) in items"
      :key="i"
      class="galeria-item"
      :class="{ activo: active === i }"
      tabindex="0"
      @pointerenter="onEnter($event, i)"
      @click="onClick($event, i)"
      @keydown.enter.prevent="toggle(i)"
      @keydown.space.prevent="toggle(i)"
    >
      <img
        :src="item.img"
        :alt="item.alt || item.name || ''"
        class="galeria-img"
        loading="lazy"
        draggable="false"
      />

      <div class="galeria-info">
        <h3 v-if="item.name" class="galeria-nombre">{{ item.name }}</h3>

        <div class="galeria-texto">
          <div class="galeria-texto-inner">
            <p>{{ item.text }}</p>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

defineProps({
  /* [{ img, alt, name?, text }] */
  items: {
    type: Array,
    default: () => []
  }
})

const active = ref(null)

/* Ratón: se expande al pasar por encima (como el CodePen) */
const onEnter = (event, index) => {
  if (event.pointerType === 'mouse') active.value = index
}

/* Táctil / teclado: se abre y se cierra tocando */
const onClick = (event, index) => {
  if (event.pointerType === 'mouse') {
    active.value = index
  } else {
    toggle(index)
  }
}

const toggle = (index) => {
  active.value = active.value === index ? null : index
}
</script>

<style scoped>
.galeria {
  /* ====== ESTILOS DE TEXTO (cámbialos aquí) ====== */
  --galeria-fuente-nombre: 'elden', serif;
  --galeria-color-nombre: #ffbf00;
  --galeria-fuente-texto: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
  --galeria-color-texto: #f5f5f5;
  --galeria-color-capitular: #ffbf00;

  /* ====== TAMAÑOS ====== */
  --galeria-h: clamp(26rem, 75vh, 44rem);
  --abierto: min(34rem, 85dvh);
  --alto-max: var(--galeria-h);

  list-style: none;
  margin: 0 auto;
  padding: 0;
  display: flex;
  gap: 1rem;
  width: 100%;
  max-width: 1100px;
  height: var(--galeria-h);
}

/* ---------- Cada panel ---------- */
.galeria-item {
  position: relative;
  flex: 2 1 0;
  min-width: 0;
  overflow: hidden;
  border-radius: 1.5rem;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.6);
  cursor: pointer;
  outline: none;
  transition: flex-grow 0.5s ease-out;
}

.galeria-item.activo {
  flex-grow: 6;
}

.galeria-item:focus-visible {
  box-shadow: 0 0 0 3px #ffbf00, 0 20px 40px rgba(0, 0, 0, 0.6);
}

/* Degradado para que se lea el texto */
.galeria-item::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to top,
    rgba(0, 0, 0, 0.88) 0%,
    rgba(0, 0, 0, 0.4) 45%,
    transparent 75%
  );
  pointer-events: none;
}

.galeria-img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.95);
  transition: filter 0.5s ease-out, transform 0.8s ease-out;
}

.galeria-item.activo .galeria-img {
  filter: brightness(0.6);
  transform: scale(1.04);
}

/* ---------- Nombre + texto ---------- */
.galeria-info {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
  padding: 1.25rem;
  color: var(--galeria-color-texto);
  text-align: center;
}

.galeria-nombre {
  margin: 0;
  font-family: var(--galeria-fuente-nombre);
  font-size: 1.4rem;
  letter-spacing: 0.08rem;
  color: var(--galeria-color-nombre);
  text-shadow: 0 2px 10px rgba(0, 0, 0, 0.9);
}

/* Truco grid: 0fr -> 1fr anima la altura sin conocerla */
.galeria-texto {
  display: grid;
  grid-template-rows: 0fr;
  opacity: 0;
  transition: grid-template-rows 0.5s ease-out, opacity 0.35s ease-out;
}

.galeria-item.activo .galeria-texto {
  grid-template-rows: 1fr;
  opacity: 1;
  transition-delay: 0.15s;
}

.galeria-texto-inner {
  min-height: 0;
  overflow-y: auto;
  max-height: calc(var(--alto-max) - 6.5rem);
  overscroll-behavior: contain;
}

.galeria-texto p {
  margin: 0.6rem 0 0;
  font-size: var(--lore-size, 1rem);
  font-family: var(--galeria-fuente-texto);
  color: var(--galeria-color-texto);
  line-height: 1.5;
  text-align: center;
  hyphens: auto;
}

/* Letra capitular dorada con la fuente 'elden' (igual que .txt-lore) */
.galeria-texto p::first-letter {
  font-size: 3em;
  font-family: 'elden';
  color: var(--galeria-color-capitular);
}

/* ---------- Tablet ---------- */
@media (max-width: 991.98px) {
  .galeria {
    gap: 0.75rem;
  }

  .galeria-item {
    border-radius: 1.25rem;
  }

  .galeria-nombre {
    font-size: 1.15rem;
  }
}

/* ---------- Móvil: paneles apilados, se abren en altura ---------- */
@media (max-width: 767.98px) {
  .galeria {
    flex-direction: column;
    height: auto;
    gap: 0.75rem;
    --alto-max: var(--abierto);
  }

  .galeria-item {
    flex: none;
    height: 11rem;
    transition: height 0.5s ease-out;
  }

  .galeria-item.activo {
    flex-grow: 0;
    height: var(--abierto);
  }
}

@media (prefers-reduced-motion: reduce) {
  .galeria-item,
  .galeria-img,
  .galeria-texto {
    transition: none;
  }
}
</style>