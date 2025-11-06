<template>
  <div class="center-box">
    <h1>Llistat de Tasques</h1>

    <TaskForm @afegir="afegirNova"/>

    <div class="checkbox-container">
      <input type="checkbox" v-model="veurePendents" id="veurePendents" />
      <label for="veurePendents">Mostra només pendents</label>
    </div>

    <TaskList :tasques="tasquesVisibles" @toggle="alternarEstat" @borrar="borrarTasca"/>

    <p class="stats">Total: {{ total }} | Pendents: {{ pendents }}</p>
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
  const id = llistaTasques.value.length ? llistaTasques.value.at(-1).id + 1: 1;
  llistaTasques.value.push({ id, titol: text, feta: false });
};

const borrarTasca = (id) => {
  llistaTasques.value = llistaTasques.value.filter(t => t.id !== id);
};

const alternarEstat = (id) => {
  const t = llistaTasques.value.find(t => t.id === id);
  t.feta = !t.feta;
};

const tasquesVisibles = computed(() =>
  veurePendents.value ? llistaTasques.value.filter(t => !t.feta) : llistaTasques.value
);

const total = computed(() => llistaTasques.value.length);
const pendents = computed(() => llistaTasques.value.filter(t => !t.feta).length);

</script>