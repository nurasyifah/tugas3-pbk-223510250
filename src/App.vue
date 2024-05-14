<template>
  <h1 class="mt-3 text-center">App To Do List</h1>
  <h2 class="mt-3 text-center">My Activity Schedule @nurasyifah_</h2>
  <div class="todo-app">
    <input type="text" class="todo-input" placeholder="type here" v-model="newTodo" @keydown.enter.prevent="addTodo">
    <button class="todo-btn" @click="addTodo">create</button>
    <ul class="todo-list">
      <li v-for="(todo, index) in todos" :key="index" class="todo-item">
        <span v-if="editIndex !== index">{{ todo.text }}</span>
        <input v-else type="text" v-model="editText">
        <button class="todo-btn" @click="editIndex !== index ? editTodoForm(index) : editTodo()">
          {{ editIndex !== index ? 'edit' : 'update' }}</button>
          <button class="todo-btn" @click="deleteTodo(todo)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: '',
      editIndex: null,
      editText: ''
    };
  },
methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo });
        this.newTodo = '';
      }
    },
editTodoForm(index) {
      this.editIndex = index;
      this.editText = this.todos[index].text;
    },
editTodo() {
  if (this.editText.trim() !== '') {
    this.todos[this.editIndex].text = this.editText;
    this.editIndex = null;
    this.editText = '';
   }
  },
deleteTodo(todo) {
      const index = this.todos.indexOf(todo);
      if (index !== -1) {
        this.todos.splice(index, 1);
      }
    }
  }
};  
</script>

<style>
body {
  background-color: skyblue;
}

.todo-app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f4f4f4;
  border-radius: 5px;
}

.todo-title {
  font-size: 24px;
  margin-bottom: 10px;
}

.todo-input {
  width: calc(100% - 70px);
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid skyblue;
  border-radius: 3px;
}

.todo-btn {
  padding: 8px 12px;
  margin-left: 10px;
  background-color: skyblue;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.todo-list {
  list-style-type: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #ccc;
}

.todo-item:last-child {
  border-bottom: none;
}

.todo-input {
  text-align: center; 
}

.todo-input::placeholder {
  text-align: center;
}
</style>