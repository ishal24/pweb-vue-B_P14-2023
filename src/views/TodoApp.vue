<template>
  <div class="container" style="width: 1000px;">
    <h1 class="mt-4">To-Do List</h1>

    <!-- Add New To-Do Form Row -->
    <div class="row mb-3">
      <div class="col" style="width: 15%;">
        <input class="form-control" v-model="newTodo.title" placeholder="Task title" />
      </div>
      <div class="col" style="width: 30%;">
        <textarea class="form-control" v-model="newTodo.description" placeholder="Task description"></textarea>
      </div>
      <div class="col" style="width: 15%;">
        <input type="date" class="form-control" v-model="newTodo.dueDate" />
      </div>
      <div class="col" style="width: 20%;">
        <select class="form-select" v-model="newTodo.category">
          <option value="High">High Priority</option>
          <option value="Low">Low Priority</option>
        </select>
      </div>
      <div class="col" style="width: 20%;">
        <button class="btn btn-primary" @click="addTodo">Add</button>
      </div>
    </div>

    <!-- Display Added To-Do Items -->
    <table class="table">
      <thead>
        <tr>
          <th></th>
          <th>Todo</th>
          <th>Description</th>
          <th>Due Date</th>
          <th>Priority</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td>
            <input type="checkbox" class="form-check-input" style="width: 20px;" v-model="todo.completed" />
          </td>
          <td>
            <p class="mb-0" :style="{ 'text-decoration': todo.completed ? 'line-through' : 'none' }">{{ todo.title }}</p>
          </td>
          <td>
            <p class="mb-0"><strong></strong> {{ todo.description }}</p>
          </td>
          <td>
            <p class="mb-0"><strong></strong> {{ todo.dueDate }}</p>
          </td>
          <td>
            <p class="mb-0"><strong></strong> {{ todo.category }}</p>
          </td>
          <td>
            <button class="btn btn-info" @click="showEditDialog(index)">Edit</button>
            <button class="btn btn-danger" @click="deleteTodo(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>

    <div>
      <button class="btn" @click="removeCompletedTodos">remove completed todos</button>
    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue';

const todos = ref([]);

// State for adding a new todo
const newTodo = ref({
  title: '',
  description: '',
  dueDate: '',
  category: 'High',
});

// State for editing todo
// const editingIndex = ref(-1);

// Function to add a new todo
function addTodo() {
  if (newTodo.value.title.trim() !== '') {
    todos.value.push({ ...newTodo.value, editing: false });
    resetNewTodo();
  }
}

// Function to delete a todo
function deleteTodo(index) {
  todos.value.splice(index, 1);
}

// Function to reset the newTodo state
function resetNewTodo() {
  newTodo.value.title = '';
  newTodo.value.description = '';
  newTodo.value.dueDate = '';
  newTodo.value.category = 'High';
}

// Function to remove completed todos
function removeCompletedTodos() {
  todos.value = todos.value.filter((todo) => !todo.completed);
}
</script>