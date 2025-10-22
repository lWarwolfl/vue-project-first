<script setup lang="ts">
import { computed, ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";
import type { TTask } from "./types";

const tasks = ref<TTask[]>([]);
const totalDone = computed(
  () => tasks.value.filter((item) => item.done).length
);

function addTask(newTask: string) {
  tasks.value.push({ id: crypto.randomUUID(), title: newTask, done: false });
}

function toggleTask(id: string) {
  const toggleIndex = tasks.value.findIndex((item) => item.id === id);

  if (tasks.value[toggleIndex])
    tasks.value[toggleIndex].done = !tasks.value[toggleIndex].done;
}

function removeTask(id: string) {
  const toggleIndex = tasks.value.findIndex((item) => item.id === id);

  if (toggleIndex !== -1) tasks.value.splice(toggleIndex, 1);
}
</script>

<template>
  <main>
    <h3>Tasks App</h3>

    <TaskForm @add-task="addTask" />

    <h4 v-if="!tasks.length">Create a new task.</h4>
    <h4 v-else>{{ totalDone }} / {{ tasks.length }} tasks completed</h4>

    <TaskList :tasks @toggle-done="toggleTask" @remove-task="removeTask" />
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 1rem auto;
  padding: 16px;
  
}

.button-container {
  display: flex;
  justify-content: end;
}
</style>
