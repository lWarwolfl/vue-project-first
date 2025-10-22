<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{ addTask: [newTask: string] }>();

const newTask = ref("");
const error = ref("");

function onSubmit() {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value);
    newTask.value = "";
  } else {
    error.value = "Task is invalid!";
  }
}
</script>

<template>
  <form @submit.prevent="onSubmit">
    <label>
      New Task
      <input
        @input="error = ''"
        v-model="newTask"
        :aria-invalid="!!error || undefined"
      />

      <small id="invalid-helper" v-if="error">{{ error }}</small>
    </label>

    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
