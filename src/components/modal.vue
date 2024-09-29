<template>
  <div v-if="open" class="modal" @click="$emit('close')">
    <div class="content" @click.stop>
      <p>Confirm Modal</p>
      <hr />
      <slot />
      <hr />
      <slot name="actions" :confirm="confirm">
        <button @click="close">close</button>
        <button @click="confirm">OK</button>
      </slot>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onBeforeUnmount } from "vue";

const props = defineProps({
  open: { type: Boolean, default: false },
});
const emits = defineEmits({
  close() {
    null;
  },
  confirm() {
    null;
  },
});

function close() {
  emits("close");
}
function confirm() {
  emits("confirm");
}
function handleKeydown(e) {
  if (props.open && e.key === "Escape") {
    close();
  }
}

onMounted(() => {
  document.addEventListener("keydown", handleKeydown);
});

onBeforeUnmount(() => document.removeEventListener("keydown", handleKeydown));
</script>

<style>
.modal {
  width: 100%;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.75);
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  top: 0px;
  left: 0px;
}
.content {
  background: red;
}
</style>
