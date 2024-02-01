<template>
  <h1>Todo List</h1>
  <div>
    <input v-model='todo' type='text' placeholder='할 일을 작성해주세요.' />
    <button type='button' @click='createTodo'>추가</button>
  </div>
  <ul>
    <li v-for='(todo, index) in todoList' :key='index'>
      <input type='checkbox' v-model='todo.isChecked' />
      <span
        :class='{ isCompleted: todo.isChecked }'
      >
        {{ todo.name }}
      </span>
      <button type="button" @click="deleteTodo(index)">삭제</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      todo: '',
      todoList: [],
    }
  },
  methods: {
    createTodo() {
      if (this.todo.trim() !== '') {
        const todo = {
          name: this.todo,
          isUpdate: false,
          isChecked: false,
        }
        this.todoList.push(todo);

        // 초기화
        this.todo = ''
      }
    },
    updateTodo() {},
    deleteTodo(i) {
      this.todoList = this.todoList.filter((_, index) => index !== i)
    },
  }
}
</script>

<style lang="scss" scoped>
.isCompleted {
  text-decoration: line-through;
}
</style>
