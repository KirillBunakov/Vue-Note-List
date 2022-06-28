<template>
  <div id="app">
      <h1>Todo Application</h1>
      <AddTodo
        @add-todo="addTodo"
      />
      <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
      </select>
      <hr>
      <Loader v-if="loading"/>
      <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
      />
      <p v-else>No Todos</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList"
import AddTodo from "@/components/AddTodo"
import Loader from "@/components/Loader"


export default {
  name: 'App',
  data() {
    return {
      todos: [
        {id:1, title: 'Купить хлеб', completed:false},
        {id:2, title: 'Купить масло', completed:false},
        {id:3, title: 'Купить пиво', completed:false}
      ],
      loading: true,
      filter: 'all'
    }
  },
  computed: {
    filteredTodos(){
      if (this.filter === 'all') {
        return this.todos
      }
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    TodoList: TodoList, AddTodo , Loader
},
mounted() {
  this.loading = false
}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
