<template>
  <li class="task">
    <span :style="{ textDecoration: tasca.feta ? 'line-through' : 'none' }">{{ tasca.titol }}</span>

    <div class="task-buttons">
      <button class="complete" @click="emit('toggle', tasca.id)">{{ tasca.feta ? "Desmarcar" : "Completar" }}</button>

      <button class="delete" @click="emit('borrar', tasca.id)">
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