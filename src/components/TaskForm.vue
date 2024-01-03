<script setup>
import { ref, inject } from 'vue';

const txtTask = ref("");
const tasks   = inject('tasks');

const addTask = (e) => {
  e.preventDefault();

  if (txtTask.value.trim() !== "") 
  {
    tasks.value.unshift({ description: txtTask.value.trim(), completed: false });
  } 
  else 
  {
    alert("Task field cannot be blank!");
  }

  txtTask.value = "";
}
</script>

<template>
  <form class="w-100" @submit="addTask">
    <div class="card card-form">
      <div class="card-body">
        <div class="mb-3">
          <label class="form-label">Task</label>
          <input type="text" class="form-control" v-model="txtTask">
        </div>

        <button type="submit" class="btn btn-primary w-100">Add Task</button>
      </div>
    </div>
  </form>
</template>