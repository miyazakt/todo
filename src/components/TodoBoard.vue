<template>
  <div class="hello">
    <div class="input-form">
      <input class="form-control" type="text" v-model="todoTitle" placeholder="やること" />
      <textarea rows="10" class="form-control" v-model="todoContent"></textarea>
      <input class="form-control" type="date" v-model="todoDate" />
      <input class="form-control" type="time" v-model="todoTime" />
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
    let date = new Date()
    var zerofill = function (val) {
      if (val.toString().length === 1) {
        return `0${val}`
      }
      return val
    }
    let year = date.getFullYear()
    let month = zerofill(date.getMonth() + 1)
    let day = zerofill(date.getDate())

    return {
      todoTitle: '',
      todoContent: '',
      todoDeadline: '',
      todoDate: `${year}-${month}-${day}`,
      todoTime: `12:00`,
      todos: []
    }
  },
  mounted () {
    let todos = JSON.parse(localStorage.getItem('todos')) || []
    console.log('hoge')
    this.todos = todos.map((todo) => {
      todo.deadline = new Date(todo.deadline)
      return todo
    })
  },
  methods: {
    add () {
      let todo = this.createTodo(this)
      todo.deadline = new Date(this.todoDate + ' ' + this.todoTime)
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
  margin: 7px auto;
  width: 95%;
}
ol {
  padding: 0;
}
</style>
