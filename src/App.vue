<template>
  <button @click="openModal">open</button>
  <modalComponent
    :open="isOpen"
    @close="isOpen = false"
    @confirm="confirmModal"
  >
    <strong>You sure?</strong>
    <template #actions="{ confirm }">
      Enter
      <input :placeholder="CONFIRMATION_TEXT" v-model="confirmInput" />
      &nbsp
      <button @click="confirm" :disabled="!isConfirmationCorrect">
        Confirm
      </button>
    </template>
  </modalComponent>
</template>

<script setup>
import modalComponent from "./components/modal.vue";
import { ref, computed } from "vue";

const CONFIRMATION_TEXT = "CONFIRM";
const isOpen = ref(false);
const confirmInput = ref("");
const isConfirmationCorrect = computed(
  () => confirmInput.value === CONFIRMATION_TEXT
);

function openModal() {
  confirmInput.value = "";
  isOpen.value = true;
}
function confirmModal() {
  alert("OK!");
  isOpen.value = false;
}
function confirmClose() {
  isOpen.value = false;
}
</script>

<style></style>