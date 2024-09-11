<template>
  <li>
    <button @click="$emit('complete')" :class="className">
      {{ props.task.title }}
    </button>
    <button @click="$emit('remove')"><i class="far fa-trash-alt"></i>-</button>
  </li>
</template>
<script setup>
import { defineProps, computed } from "vue";
const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
});
const className = computed(() => {
  let classes = ["toggle"];
  if (props.task.completed) {
    classes.push("toggle-completed");
  }
  return classes;
});
</script>
