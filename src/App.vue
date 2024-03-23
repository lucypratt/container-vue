<script lang="ts">
interface Todo {
  id: number;
  todo: string;
  completed: boolean;
}
export default {
  data() {
    return {
      todos: [
        { id: 1, todo: "Internship Hours", completed: false },
        { id: 2, todo: "Homework", completed: true },
      ] as Todo[],
      newTodo: "",
      editingTodo: null as Todo | null,
    }
  },
  methods: {
    getNextId() {
      let lastId = 0
      
    for (const todo of this.todos) {
    if (todo.id > lastId) {
      lastId = todo.id
    }
  }
  
      return lastId + 1
    },
    
    
    addTodo() {
  if (this.newTodo !== "") {
    this.todos.push({
      id: this.getNextId(),
      todo: this.newTodo,
      completed: false,
    })
    this.newTodo = ""
  }
},
    editTodo(todo: any) {
      this.editingTodo = todo as any
    },
    saveTodo() {
      this.editingTodo = null as any
    },
    deleteTodo(index: any) {
      this.todos.splice(index, 1)
    },
    clearCompletedTodos() {
      this.todos = this.todos.filter((todo) => !todo.completed)
    },
    remainingTodos() {
    return this.todos.filter((todo) => !todo.completed).length
  },
  }
 
}
</script>

<template>
  <div>
    <h1>Todo App</h1>
    <div>
      <input v-model="newTodo" v-on:keyup.enter="addTodo" placeholder="Add a new todo" />
      <button v-on:click="addTodo">Add</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <span v-if="editingTodo !== todo">
          <input type="checkbox" v-model="todo.completed" />
          <span v-on:click="editTodo(todo)">{{ todo.todo }}</span>
          <button v-on:click="deleteTodo(index)">Delete</button>
        </span>
        <span v-else>
          <input v-model="todo.todo" v-on:keyup.enter="saveTodo()" />
          <button v-on:click="saveTodo()">Save</button>
        </span>
      </li>
    </ul>
    <div>
      <p>{{ remainingTodos() }} todos left to complete</p>
    </div>
    <button v-on:click="clearCompletedTodos">Clear completed todos</button>
  </div>
</template>

<style>

</style>
