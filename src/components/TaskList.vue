<script setup lang="ts">
import type { TTask } from "../types";

defineProps<{
  tasks: TTask[];
}>();
</script>

<template>
  <article v-for="task in tasks" :key="task.id">{{ task.title }}</article>
</template>
