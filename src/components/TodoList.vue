<template>
    <div>
      <h1>My To-Do List</h1>
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add a new task" />
      <ul>
        <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
          {{ task.title }}
          <button @click="toggleCompletion(task)">Toggle Complete</button>
          <button @click="deleteTask(index)">Delete</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    name: 'TodoList',
    setup() {
      const newTask = ref('');
      const tasks = ref([]);
  
      const addTask = () => {
        if (newTask.value.trim()) {
          tasks.value.push({ title: newTask.value, completed: false });
          newTask.value = '';
        }
      };
  
      const toggleCompletion = (task) => {
        task.completed = !task.completed;
      };
  
      const deleteTask = (index) => {
        tasks.value.splice(index, 1);
      };
  
      return { newTask, tasks, addTask, toggleCompletion, deleteTask };
    }
  };
  </script>
  
  <style>
  .completed {
    text-decoration: line-through;
  }
  </style>
  