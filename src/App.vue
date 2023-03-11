<template>
  <main>
    <header>
      <img src="https://pinia.vuejs.org/logo.svg" alt="logo">
      <h1>Piniaa Task</h1>
    </header>
    <div class="new-task-form">
      <TaskForm />
    </div>

    <nav class="filter">
      <button :class="{ 'active': filter === 'all' }" @click="filter = 'all'">All task</button>
      <button :class="{ 'active': filter === 'favs' }" @click="filter = 'favs'">Favorite</button>
    </nav>

    <div v-if="loading" class="loading">
      Loading tasks....
    </div>

    <div class="task-list" v-if="filter === 'all'">
      <p>You have {{ totalCount }} task left todo</p>
      <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>You have {{ favCount }} task left todo</p>
      <div v-for="task in favs" :key="task.id">
        <TaskDetails :task="task" />
      </div>
    </div>

    <button class="reset__button" @click="taskStore.$reset">reset</button>

  </main>
</template>
<script setup>
import { storeToRefs } from 'pinia';
import { ref } from 'vue';
import TaskDetails from './components/TaskDetails.vue';
import TaskForm from './components/TaskForm.vue';
import { useTaskStore } from './stores/TaskStore';
const taskStore = useTaskStore();
const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

taskStore.getTasks()
const filter = ref('all')
</script>

