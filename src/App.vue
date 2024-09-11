<template>
  <nav>
    <div id="app">
      <task-comp
        :tasks="tasks"
        :incomplete="incomplete"
        :newTask="newTask"
        @clearAll="clear"
        @clearCompleted="clearCompleted"
        @add="addTask"
      />
    </div>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view />
</template>
<script setup>
import { ref, computed } from "vue";
import taskComp from "./components/taskComp.vue";
//clear all
const clear = () => {
  tasks.value = [""];
};
//const rt = tasks.length;
//-------------------------------------
const incomplete = computed(() => {
  return tasks.value.filter(inProgress).length;
});
const inProgress = (task) => {
  return !isCompleted(task);
};
const isCompleted = (task) => {
  const completed = task.completed;
  return completed;
};
const clearCompleted = () => {
  tasks.value = tasks.value.filter(inProgress);
};
//--------------------------------------------------
function addTask(taskTitle) {
  tasks.value.push({
    title: taskTitle,
    completed: false,
  });
}
/*const addTask = (newtask) => {
  if (newTask.value) {
    tasks.value.push({
      title: newTask.value,
      completed: false,
    });
    newTask = "";
    console.log("new task is" + newTask.value);
    console.log("jjjjjjjj");
  }
};*/
// Define reactive tasks state
const tasks = ref([
  { id: 1, title: "Learn Vue JS", completed: true },
  { id: 2, title: "Watch Netflix", completed: true },
  { id: 3, title: "Go shopping", completed: false },
  { id: 4, title: "Learn guitar", completed: false },
  { id: 5, title: "Send email", completed: false },
]);
//const newTask = ref("");
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
