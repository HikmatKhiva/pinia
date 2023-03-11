<template>
    <div class="task">
        <h3>{{ task.title }}</h3>
        <div class="icons">
            <i @click="taskStore.deleteTask(task.id)" class="fa-solid fa-trash"></i>
            <i :class="{ active: task.isFav }" @click="taskStore.toggleFav(task.id)" class="fa-solid fa-heart"></i>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
import { useTaskStore } from '../stores/TaskStore';
const taskStore = useTaskStore()
const props = defineProps({
    task: {
        type: Object,
    }
})

</script>
