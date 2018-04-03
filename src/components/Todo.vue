<template>
  <div class="card">
    <div class="card-title">{{ title }}</div>
    <span>内容</span>
    <div class="card-content">
      <p>{{ content }}</p>
    </div>
    <div class="card-right card-deadline">
      <span>期限: </span>
      <span>
      {{ deadline }}
      </span>
    </div>
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
      var zerofill = function (val) {
        if (val.toString().length === 1) {
          return `0${val}`
        }
        return '' + val
      }
      let date = this.todo.deadline
      if (Object.prototype.toString.call(date) !== '[object Date]') {
        return this.todo.deadline
      }
      let year = date.getFullYear()
      let month = zerofill(date.getMonth() + 1)
      let day = zerofill(date.getDate())
      let hours = zerofill(date.getHours())
      let minutes = zerofill(date.getMinutes())
      return `${year}-${month}-${day} ${hours}:${minutes}`
    }
  },
  props: ['todo']
}
</script>

<style scoped>
.card {
  margin: 5px;
  padding: 5px;
  border: 1px solid black;
}
.card-right {
  text-align: right;
}

.card-title {
  margin: 3px;
}

.card-content {
  padding: 3px;
  border-top: 1px gray solid;
  border-bottom: 1px gray solid;
}

.card-deadline {
  margin: 3px;
}
</style>
