<template>
  <ul style="list-style: none; padding: 0; width: 100%">
    <TaskItem v-for="t in tasques" :key="t.id" :tasca="t" @toggle="emit('toggle', $event)" @borrar="emit('borrar', $event)"/>
  </ul>
</template>

<script setup>

import TaskItem from "./TaskItem.vue";

defineProps({
  tasques: Array
});

const emit = defineEmits(["toggle", "borrar"]);

</script>