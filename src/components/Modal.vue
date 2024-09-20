<template>
  <transition name="modal-fade">
    <div class="modal-overlay" v-if="show" @click.self="closeModal">
      <div class="modal-content">
        <button class="modal-close" @click="closeModal">X</button>
        <slot></slot>
      </div>
    </div>
  </transition>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  show: Boolean
});

const emit = defineEmits(['close']);

const closeModal = () => {
  emit('close');
};
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
}

.modal-content {
  background: rgba(0, 0, 0, 0);
  padding: 8em;
  border-radius: 8px;
  position: relative;
  width: 100%;
  background-size: cover;
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 20px;
  cursor: pointer;
  color: aliceblue;
}

/* Transiciones */

.modal-fade-enter-active, .modal-fade-leave-active {
  transition: opacity 0.5s;
}
.modal-fade-enter, .modal-fade-leave-to {
  opacity: 0;
 
}
.modal-fade-enter-to, .modal-fade-leave {
  opacity: 1;

}
</style>