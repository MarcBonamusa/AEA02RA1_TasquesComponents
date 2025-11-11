<template>
  <li class="tasca">
    <span :style="{ textDecoration: tasca.feta ? 'line-through' : 'none' }">{{ tasca.titol }}</span>

    <div class="tascaBotons">
      <button class="completar" @click="emit('toggle', tasca.id)">{{ tasca.feta ? "Desmarcar" : "Completar" }}</button>

      <button class="esborrar" @click="emit('borrar', tasca.id)">
        <i class="fas fa-trash"></i>
      </button>
    </div>
  </li>
</template>

<script setup>

defineProps({
  tasca: Object
});

const emit = defineEmits(["toggle", "borrar"]);

</script>