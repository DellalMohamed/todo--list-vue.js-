<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input type="text" placeholder="New Task" v-model="localNewTask" />
        <button @click="addTaskkk"><i class="fas fa-plus">+</i></button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <taskItem
            @complete="completeTask(task)"
            @remove="removeItem(ind)"
            v-for="(task, ind) in props.tasks"
            :key="ind"
            :task="task"
          />
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="emitClearCompleted">Clear completed</button>
        <button @click="clearAll">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ incomplete }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import taskItem from "./taskItem.vue";
import { defineProps, defineEmits, ref, computed } from "vue";
const props = defineProps({
  tasks: {
    type: Array,
  },
  incomplete: {
    type: Number,
  },
  newTask: {
    type: Object,
    default: () => ({}),
  },
});
const allTasks = computed(() => props.tasks); /*******************/
const all_emits = defineEmits([
  "clearAll",
  "emitClearCompleted",
  "inProgress",
  "addTask",
]);
//   add task
const localNewTask = ref("");
function addTaskkk() {
  if (localNewTask.value.trim()) {
    all_emits("add", localNewTask.value);
    localNewTask.value = ""; // Clear the input field after adding
  }
}
// Function to emit the 'clearAll' event
function clearAll() {
  all_emits("clearAll");
}
function emitClearCompleted() {
  all_emits("clearCompleted");
}
function removeItem(ind) {
  allTasks.value.splice(ind, 1);
}
function completeTask(task) {
  task.completed = !task.completed;
}
</script>
