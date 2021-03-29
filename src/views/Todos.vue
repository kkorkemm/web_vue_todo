<template>
  <div>
    <h2>ToDo List</h2>
    <router-link to='/'>Home</router-link>
    <AddTodo
      @add-todo='addTodo'
    />
    <select class="filter-select" v-model='filter'>
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not completed</option>
    </select>
    <Loader v-if='loading' />
    <TodoList
        v-else-if='filtered.length'
        v-bind:todos='filtered'
        @remove-todo="removeTodo"
    />
    <p v-else>ToDo List is empty!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
    .then(json => {
        setTimeout(() => {
            this.todos = json
            this.loading = false
        }, 200)
    })
  },
  computed: {
      filtered() {
          if (this.filter === 'all') {
              return this.todos
          }
          else if (this.filter === 'completed') {
              return this.todos.filter(t => t.completed)
          }
          else {
              return this.todos.filter(t => !t.completed)
          }
      }
  },
  components: {
    TodoList, AddTodo, Loader
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    } 
  }
}
</script>

<style scoped>

    .filter-select {
        outline: none;
        padding: 5px;
        border: none;
        border-radius: 5px;
        background: #8d8fad;
        margin: 20px 0;
        color: #fff;
        font-size: 1rem;
        cursor: pointer;
    }

</style>