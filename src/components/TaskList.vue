<script setup lang="ts">
import type { TTask } from "../types";

defineProps<{
  tasks: TTask[];
}>();

const emit = defineEmits<{
  toggleDone: [id: string];
  removeTask: [id: string];
}>();
</script>

<template>
  <TransitionGroup name="list" tag="div">
    <article class="task" v-for="task in tasks" :key="task.id">
      <input
        :id="task.id"
        @input="emit('toggleDone', task.id)"
        type="checkbox"
      />

      <span :class="{ done: task.done }">{{ task.title }}</span>

      <button @click="emit('removeTask', task.id)" class="outline remove">
        Remove
      </button>
    </article>
  </TransitionGroup>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.task {
  display: flex;
  align-items: center;
}

.remove {
  margin-left: auto;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(100px);
}
</style>
