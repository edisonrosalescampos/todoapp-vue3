<script setup>
import TaskItem from './TaskItem.vue';

defineProps({
    tasks: Array
})
</script>

<template>
    <div class="text-white text-center" v-if="tasks.length === 0">No pending tasks to show</div>
    <div class="task-list" v-else>
        <TaskItem v-for="item in tasks" :task="item" :key="item.description" />
    </div>
</template>