<script setup lang="ts">
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import type { TTask } from "./types";

const tasks = ref<TTask[]>([]);

function addTask(newTask: string) {
  tasks.value.push({ id: crypto.randomUUID(), title: newTask, done: false });
}
</script>

<template>
  <main>
    <h3>Tasks App</h3>

    <TaskForm @add-task="addTask" />

    <TaskList :tasks />
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 1rem auto;
}

.button-container {
  display: flex;
  justify-content: end;
  margin-bottom: 1rem;
}
</style>
