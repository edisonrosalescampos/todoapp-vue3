<script setup>
import { inject } from 'vue';

defineProps({
  task: Object
});

const tasks = inject('tasks');

const deleteTask = (task) => {
  tasks.value = tasks.value.filter(item => item.description !== task);
}
const changeTaskStatus = (task, completed) => {
  tasks.value = tasks.value.map(item => {
    if (item.description === task) 
    {
      item.completed = completed;
    }

    return item;
  });
}
</script>

<template>
  <div class="card">
    <div class="card-body">
      <div class="form-check">
        <input type="checkbox" class="form-check-input" @change="changeTaskStatus(task.description, !task.completed)">
        <label class="form-check-label">
          <span class="me-2">{{ task.description }}</span>
          <span class="badge bg-success px-1" v-if="task.completed">completed</span>
          <span class="badge bg-danger px-1" v-else>pending</span>
        </label>
      </div>

      <button type="button" class="btn btn-danger btn-sm" @click="deleteTask(task.description)">
        <i class="fa fa-trash"></i>
      </button>
    </div>
  </div>
</template>