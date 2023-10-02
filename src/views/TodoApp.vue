<template>
  <div>
    <h1>Plan of Attack</h1>
    <h6>Oh dark, I have to do these to-do lists!</h6>
    <div>
      <input v-model="newTodo.text" placeholder="I have to do" />
      <select v-model="newTodo.category">
        <option value="High">High Priority</option>
        <option value="Low">Low Priority</option>
      </select>
      <button @click="addTodo">Add</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <label>
          <input type="checkbox" v-model="todo.completed" />
        </label>
        <span :class="{ 'High': todo.category === 'High', 'completed': todo.completed }">{{ todo.text }}</span>
        <button @click="editTodo(index)">Edit</button>
        <button @click="deleteTodo(index)">Delete</button>
        <form v-if="todo.editing" @submit="saveTodo(index)">
          <input v-model="todo.text" />
          <button type="submit">Save</button>
        </form>
      </li>
    </ul>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  const todos = ref([
    { text: 'Sisop', category: 'High', editing: false, completed: false },
    { text: 'Tidur', category: 'Low', editing: false, completed: false },
  ]);

  const newTodo = ref({
    text: '',
    category: 'High',
    completed: false,
  });

  function addTodo() {
    if (newTodo.value.text.trim() !== '') {
      todos.value.push({ ...newTodo.value, editing: false });
      newTodo.value.text = '';
      newTodo.value.category = 'High';
      newTodo.value.completed = false;
    }
  }

  function editTodo(index) {
    todos.value[index].editing = true;
  }

  function saveTodo(index) {
    todos.value[index].editing = false;
  }

  function deleteTodo(index) {
    todos.value.splice(index, 1);
  }
</script>

<style scoped>
  .completed {
    text-decoration: line-through;
  }
</style>

<style scoped>
  div {
    text-align: center;
    max-width: 400px;
    margin: 0 auto;
  }

  h1 {
    font-size: 24px;
    margin-bottom: 20px;
  }

  input {
    width: 60%;
    padding: 8px;
    margin-right: 10px;
  }

  select {
    width: 25%;
    padding: 8px;
    margin-right: 10px;
  }

  button {
    padding: 8px 12px;
    background-color: #007bff;
    color: #fff;
    border: none;
    cursor: pointer;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: 1px solid #ddd;
    padding: 10px;
    margin-bottom: 10px;
  }

  button {
    background-color: gray; 
    color: white;
    border: none;
    padding: 6px 10px;
    margin-left: 5px;
    cursor: pointer;
  }

  button:hover {
    background-color: #0D6EFD;
  }
  .High {
    font-weight: bold;
    color:#0D6EFD; 
  }
</style>