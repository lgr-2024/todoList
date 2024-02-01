<template>
  <TodoList msg="Welcome to Your Vue.js App"/>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
@import '@/assets/styles/reset.css'
</style>
