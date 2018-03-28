<template>
  <div class="hello">
    <div class="input-form">
      <input class="form-control" type="text" v-model="todoTitle" placeholder="やること" />
      <textarea rows="10" class="form-control" v-model="todoContent"></textarea>
      <input class="form-control" type="datetime-local" v-model="todoDeadline" />
      <button class="form-control" @click="add()">追加</button>
    </div>
    <ol>
      <todo-item v-for="item in todos" v-bind:todo="item"></todo-item>
    </ol>
  </div>
</template>

<script>
import Todo from './Todo'

export default {
  name: 'TodoList',
  data () {
    return {
      todoTitle: '',
      todoContent: '',
      todoDeadline: new Date(),
      todos: []
    }
  },
  mounted () {
    this.todos = JSON.parse(localStorage.getItem('todos')) || []
  },
  methods: {
    add () {
      let todo = this.createTodo(this)
      this.todos.push(todo)
      this.clearTodo()
      this.setItem()
    },
    clearTodo () {
      this.todoTitle = ''
      this.todoContent = ''
      this.todoDeadline = new Date()
    },
    setItem () {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    },
    createTodo (that) {
      return {
        title: that.todoTitle,
        content: that.todoContent,
        deadline: that.todoDeadline
      }
    }
  },
  components: {
    'todo-item': Todo
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.input-form {
}
.form-control {
  display: block;
  margin: 3px;
  width: 95%;
}
</style>
