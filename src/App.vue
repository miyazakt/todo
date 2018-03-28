<template>
  <div id="app">
    <TodoBoard/>
  </div>
</template>

<script>
import TodoBoard from './components/TodoBoard'

export default {
  name: 'App',
  components: {
    TodoBoard
  }
}
</script>

<style>
#app {
  width: 500px;
  margin: 0 auto;
  border: 1px solid black;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
