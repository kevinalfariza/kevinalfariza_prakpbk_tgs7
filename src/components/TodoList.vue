<template>
    <div class="container">
      <h1 class="title">Cucian Motor</h1>
      <input v-model="newTask" class="input" placeholder="Tambahkan antrian" @keyup.enter="addTodo" />
      <button @click="addTodo" class="button">Masukkan</button>
      <ul class="todo-list">
        <li v-for="(todo, index) in todos" :key="index" class="todo-item">
          <span :class="{ 'completed-task': todo.completed }" class="todo-text">{{ todo.task }}</span>
          <div class="button-group">
            <button @click="toggleTodo(index)" class="toggle-button">
              {{ todo.completed ? 'Batalkan' : 'Selesai' }}
            </button>
            <button @click="removeTodo(index)" class="remove-button">Hapus</button>
          </div>
        </li>
      </ul>
      <p class="unfinished-count">Yang belum di cuci: {{ unfinishedTodosCount }}</p>
    </div>
  </template>
  
  <script>
  import { ref, computed } from 'vue'
  import { useTodoStore } from '../stores/todostore.js'
  
  export default {
    setup() {
      const todoStore = useTodoStore()
      const newTask = ref('')
  
      const addTodo = () => {
        if (newTask.value.trim()) {
          todoStore.addTodo(newTask.value)
          newTask.value = ''
        }
      }
  
      const unfinishedTodosCount = computed(() => todoStore.unfinishedTodosCount)
  
      return {
        newTask,
        todos: todoStore.todos,
        addTodo,
        removeTodo: todoStore.removeTodo,
        toggleTodo: todoStore.toggleTodo,
        unfinishedTodosCount
      }
    }
  }
  </script>
  
  <style scoped>
 .container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: rgba(0, 0, 255, 0.5); 
  border-radius: 8px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

  
  .title {
    color: white;
    margin-bottom: 20px;
    font-size: 24px;
    text-align: center;
  }
  
  .input {
    width: calc(100% - 120px);
    padding: 10px;
    border: 2px solid #007bff;
    border-radius: 4px;
    margin-bottom: 20px;
    font-size: 16px;
  }
  
  .button {
    width: 100px;
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
  }
  
  .button:hover {
    background-color: #0056b3;
  }
  
  .todo-list {
    list-style: none;
    padding: 0;
  }
  
  .todo-item {
    color: white;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 10px;
  }
  
  .todo-text {
    flex: 1;
  }
  
  .completed-task {
    text-decoration: line-through;
  }
  
  .button-group {
    display: flex;
  }
  
  .toggle-button,
  .remove-button {
    padding: 8px 16px;
    margin-left: 10px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 14px;
  }
  
  .toggle-button {
    background-color: #28a745;
    color: #fff;
  }
  
  .toggle-button:hover {
    background-color: #218838;
  }
  
  .remove-button {
    background-color: #dc3545;
    color: #fff;
  }
  
  .remove-button:hover {
    background-color: #c82333;
  }
  
  .unfinished-count {
    color: white ;;
    margin-top: 20px;
    font-size: 16px;
    text-align: center;
  }
  </style>
  