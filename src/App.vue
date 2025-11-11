<template>
  <div class="container">
    <h1>Llistat de Tasques</h1>

    <TaskForm @afegir="afegirNova"/>

    <div class="checkboxContainer">
      <input type="checkbox" v-model="veurePendents" id="veurePendents" />
      <label for="veurePendents">Mostra només pendents</label>
    </div>

    <TaskList :tasques="tasquesVisibles" @marcar="alternarEstat" @borrar="borrarTasca"/>

    <p class="comptador">Total: {{ total }} | Pendents: {{ pendents }}</p>
  </div>
</template>

<script setup>

import { ref, computed } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import "@fortawesome/fontawesome-free/css/all.min.css";
import "./style.css";

const llistaTasques = ref([
  { id: 1, titol: "Tasca 1", feta: true },
  { id: 2, titol: "Tasca 2", feta: false },
  { id: 3, titol: "Tasca 3", feta: false },
  { id: 4, titol: "Tasca 4", feta: false },
]);

const veurePendents = ref(false);

const afegirNova = (text) => {
  const maxId = llistaTasques.value.length ? Math.max(...llistaTasques.value.map(tasques => tasques.id)) : 0;
  llistaTasques.value.push({ id: maxId + 1, titol: text, feta: false });
};

const borrarTasca = (id) => {
  llistaTasques.value = llistaTasques.value.filter(tasques => tasques.id !== id);
};

const alternarEstat = (id) => {
  const tasques = llistaTasques.value.find(tasques => tasques.id === id);
  tasques.feta = !tasques.feta;
};

const tasquesVisibles = computed(() =>
  veurePendents.value ? llistaTasques.value.filter(tasques => !tasques.feta) : llistaTasques.value
);

const total = computed(() => llistaTasques.value.length);
const pendents = computed(() => llistaTasques.value.filter(tasques => !tasques.feta).length);

</script>