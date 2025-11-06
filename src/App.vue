<template>
  <div class="center-box">
    <h1>Llistat de Tasques</h1>

    <div class="add-task">
      <input v-model="textNova" placeholder="Afegeix una tasca nova" type="text"/>
      <button @click="afegirNova">Afegir</button>
    </div>

    <div class="checkbox-container">
      <input type="checkbox" v-model="veurePendents" id="veurePendents" />
      <label for="veurePendents">Mostra només pendents</label>
    </div>

    <ul style="list-style: none; padding: 0; width: 100%">
      <li v-for="tasca in tasquesVisibles" :key="tasca.id" class="task">
        <span :style="{ textDecoration: tasca.feta ? 'line-through' : 'none' }">{{ tasca.titol }}</span>
        <div class="task-buttons">
          <button class="complete" @click="alternarEstat(tasca)">
            {{ tasca.feta ? "Desmarcar" : "Completar" }}
          </button>
          <button class="delete" @click="borrarTasca(tasca.id)">
            <i class="fas fa-trash"></i>
          </button>
        </div>
      </li>
    </ul>

    <p class="stats">Total: {{ total }} | Pendents: {{ pendents }}</p>
    
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import "./style.css"
import "@fortawesome/fontawesome-free/css/all.min.css";

const llistaTasques = ref([
  { id: 1, titol: "Tasca 1", feta: true },
  { id: 2, titol: "Tasca 2", feta: false },
  { id: 3, titol: "Tasca 3", feta: false },
  { id: 4, titol: "Tasca 4", feta: false },
]);

const textNova = ref("");

const veurePendents = ref(false);

const afegirNova = () => {
  if (textNova.value.trim() === "") return;

  let nouIdentificador = 1;
  if (llistaTasques.value.length > 0) {
    nouIdentificador = llistaTasques.value[llistaTasques.value.length - 1].id + 1;
  }

  llistaTasques.value.push({
    id: nouIdentificador,
    titol: textNova.value,
    feta: false,
  });

  textNova.value = "";
};

const borrarTasca = (id) => {
  llistaTasques.value = llistaTasques.value.filter((item) => item.id !== id);
};

const alternarEstat = (tasca) => {
  tasca.feta = !tasca.feta;
};

const tasquesVisibles = computed(() => {
  return veurePendents.value ? llistaTasques.value.filter((t) => !t.feta) : llistaTasques.value;
});

const total = computed(() => llistaTasques.value.length);
const pendents = computed( () => llistaTasques.value.filter((t) => !t.feta).length);

</script>