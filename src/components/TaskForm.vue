<template>
  <div class="add-task">
    <input v-model="text" placeholder="Afegeix una tasca nova" type="text"/>
    <button @click="enviar">Afegir</button>
  </div>
</template>

<script setup>

import { ref } from "vue";

const emit = defineEmits(["afegir"]);

const text = ref("");

const enviar = () => {
  if (text.value.trim() === "") return;
  emit("afegir", text.value);
  text.value = "";
};

</script>