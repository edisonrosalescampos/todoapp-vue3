<script setup>
import { ref, provide } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue";

const tasks = ref([]);
provide("tasks", tasks);
</script>

<template>
  <div class="task-tracker container my-3">
    <h1 class="title">TODO APP</h1>

    <TaskForm />

    <TaskList :tasks="tasks" />
  </div>  
</template>