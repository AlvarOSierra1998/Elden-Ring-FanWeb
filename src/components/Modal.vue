<template>
  <transition name="modal-fade">
    <div class="modal-overlay" v-if="show" @click.self="closeModal">
      <div class="modal-content">
        <button class="modal-close" @click="closeModal" aria-label="Cerrar">X</button>
        <slot></slot>
      </div>
    </div>
  </transition>
</template>

<script setup>
defineProps({
  show: Boolean
})

const emit = defineEmits(['close'])

const closeModal = () => {
  emit('close')
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  overflow-y: auto;
}

.modal-content {
  background: rgba(0, 0, 0, 0);
  padding: 8em;                 /* escritorio: igual que antes */
  border-radius: 8px;
  position: relative;
  width: 100%;
  min-width: 0;
  margin: auto;                 /* centra sin recortar el principio al hacer scroll */
  background-size: cover;
  padding-bottom: 0 !important;
}

/* Tablet: menos relleno lateral */
@media (max-width: 991.98px) {
  .modal-content {
    padding: 3.5rem 1.5rem 0;
  }
}

/* Móvil: casi todo el ancho para las cartas */
@media (max-width: 767.98px) {
  .modal-content {
    padding: 3.25rem 0.5rem 0;
  }
}

.modal-close {
  position: absolute;
  top: 23px;
  right: 10px;
  z-index: 5;
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  color: aliceblue;
  transition: all 0.3s;
}

@media (max-width: 767.98px) {
  .modal-close {
    top: 10px;
    right: 8px;
    padding: 0.25rem 0.6rem;
    font-size: 22px;
  }
}

.modal-close:hover {
  background-color: aliceblue;
  color: black;
  border-radius: 20%;
}

/* Transiciones */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}
</style>