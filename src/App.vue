<script setup>
import { ref } from "vue";

const taskList  = ref([]);
const txtTask   = ref("");

const addTask = (e) => {
  e.preventDefault();

  if (txtTask.value.trim() !== "")
  {
    taskList.value.unshift({task: txtTask.value.trim(), completed: false});
  }
  else
  {
    alert("Task field cannot be blank!");
  }

  txtTask.value = "";
}
const deleteTask = (task) => {
  taskList.value = taskList.value.filter(item => item.task !== task);
}
const checkTaskDone = (task, completed) => {
  taskList.value = taskList.value.map(item => {
    if (item.task === task) 
    {
      item.completed = completed;
    }

    return item;
  });
}
</script>

<template>
  <div class="task-tracker container my-3">
    <h1 class="title">TODO APP</h1>

    <div class="card card-form">
      <div class="card-body">
        <form @submit="addTask">
          <div class="mb-3">
            <label class="form-label" for="txtTask">Task</label>
            <input type="text" class="form-control" v-model="txtTask">
          </div>
                    
          <button type="submit" class="btn btn-primary w-100">Add Task</button>
        </form>
      </div>
    </div>

    <p class="text-white text-center" v-if="taskList.length === 0">No pending tasks to show</p>

    <div class="task-list">
      <div class="card" v-for="(item, i) in taskList" :key="item.task">
        <div class="card-body">
          <div class="form-check">
            <input type="checkbox" class="form-check-input" :id="'chkTask' + item.task" @change="checkTaskDone(item.task, !item.completed)">
            <label class="form-check-label" :for="'chkTask' + item.task">
              <span class="me-2">{{ item.task }}</span>
              <span class="badge bg-success px-1" v-if="item.completed">completed</span>
              <span class="badge bg-danger px-1" v-else>pending</span>
            </label>
          </div>

          <button type="button" class="btn btn-danger btn-sm" @click="deleteTask(item.task)">
            <i class="fa fa-trash"></i>
          </button>
        </div>
      </div>

    </div>
  </div>  
</template>

<style scoped>
.card {
  width: 100%;
}
.form-check-input {
  cursor: pointer;
}
.task-tracker {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 600px;
  row-gap: 1rem;
}
.task-tracker .title {
  color: var(--bs-white);
  margin-bottom: 0;
}
.task-tracker .card {
	background-color: #333;
	color: #FFF;
	border-radius: 8px;
}
.task-tracker .card-body {
  padding: 1.25rem;
}
.task-tracker .card-form {
	border: 2px solid #151515;
  margin-bottom: 1.25rem;
} 
.task-tracker .btn {
  border-radius: 8px;
}
.task-tracker .form-control {
	background: #232323;
	border: 2px solid #151515;
	color: #fff;
	border-radius: 8px;
}
.task-list {
  display: flex;
  flex-direction: column;
  width: 100%;
  row-gap: .5rem;
}
.task-list .card-body {
	align-items: center;
	display: flex;
	justify-content: space-between;
}
</style>