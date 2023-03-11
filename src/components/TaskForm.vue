<template>
    <form @submit.prevent="handleSubmit">
        <input placeholder="new Todo" v-model="newTask" type="text">
        <button>Add</button>
    </form>
</template>

<script setup>
import { ref } from "vue";
import { useTaskStore } from "../stores/TaskStore";
const taskStore = useTaskStore();
const newTask = ref('');
const handleSubmit = () => {
    if (newTask.value.length > 0) {
        taskStore.addTask({
            title: newTask.value,
            isFav: false,
            id: Math.floor(Math.random() * 10000)
        })
        newTask.value = ''
    }
}

</script>

<style scoped></style>