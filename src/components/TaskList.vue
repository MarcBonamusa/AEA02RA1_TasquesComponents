<template>
  <ul style="list-style: none; padding: 0; width: 100%">
    <TaskItem v-for="tasca in tasques" :key="tasca.id" :tasca="tasca" @marcar="emit('marcar', $event)" @borrar="emit('borrar', $event)"/>
  </ul>
</template>

<script setup>

import TaskItem from "./TaskItem.vue";

defineProps({
  tasques: Array
});

const emit = defineEmits(["marcar", "borrar"]);

</script>