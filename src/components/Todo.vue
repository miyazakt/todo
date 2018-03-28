<template>
  <div>
    title: {{ title }}<br>
    content: {{ content }}<br>
    deadline: {{ deadline }}
  </div>
</template>

<script>
export default {
  name: 'todo-item',
  data () {
    return {
    }
  },
  computed: {
    title () {
      return this.todo.title
    },
    content () {
      return this.todo.content
    },
    deadline () {
      return this.todo.deadline
    }
  },
  props: ['todo']
}
</script>
