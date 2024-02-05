<template>
  <div class="home">
    <div class="container">
      <h1 class="title">Todo List</h1>
      <hr />
      <div class="add-input-container">
        <input v-model='todo' placeholder='할 일을 작성해주세요.' @click="createTodo" @keydown.enter="createTodo" />
        <button type="button" @click="createTodo">추가</button>
      </div>
      <hr />
      <ul class="todo-list">
        <li v-for='(todo, index) in todoList' :key='index'>
          <!-- <input type='checkbox' :isChecked="todo.isChecked" @input="todo.isChecked = !todo.isChecked" />
          <div>
            <span v-if="!todo.isUpdate" :class='{ isCompleted: todo.isChecked }'>
              {{ todo.name }}
            </span>
            <input v-else v-model="todo.name" type="text" placeholder="할 일을 작성해주세요." @keydown.esc="escEndUpdate(todo)"
              @keydown.enter="todo.isUpdate = false" />
          </div>
          <div>
            <button v-if='!todo.isUpdate' type="button" @click="startUpdate(todo, index)">수정</button>
            <button v-else type="button" @click="todo.isUpdate = false">완료</button>
            <button type="button" @click="openDeleteModal(index)">삭제</button>
          </div> -->

          <TodoItem v-model:modelValue="todo.modelValue" v-model:isUpdate="todo.isUpdate"
            v-model:isChecked="todo.isChecked" />
        </li>
      </ul>
    </div>



    <!-- <div v-if='isDeleteModal' class="modal-background">
      <div class="modal-content">
        <h2>삭제</h2>
        <hr />
        <p>정말로 삭제하시겠습니까?</p>
        <div>
          <button @click="closeDeleteModal">아니요</button>
          <button @click="deleteTodo">예</button>
        </div>
      </div>
    </div> -->
    <DeleteModal :isDeleteModal="isDeleteModal" @close-delete-click="closeDeleteModal" @delete-todo-click="deleteTodo" />

    <!-- <div v-if='isCancelModal' class="modal-background">
      <div class="modal-content">
        <h2>수정 취소</h2>
        <hr />
        <p>정말로 수정 취소하시겠습니까?</p>
        <div>
          <button @click="closeEscModal">아니요</button>
          <button @click="notUpdateTodo">예</button>
        </div>
      </div>
    </div> -->
    <CancelModal :isCancelModal="isCancelModal" @close-esc-click="closeEscModal" @not-update-todo="notUpdateTodo" />

  </div>
</template>

<script setup>
// import TodoInput from '@/components/common/TodoInput.vue'
// import TodoButton from '@/components/common/TodoButton.vue'
import DeleteModal from '@/components/DeleteModal.vue'
import CancelModal from '@/components/CancelModal.vue'
import TodoItem from '@/components/common/TodoItem.vue'
import { ref } from 'vue'

let todo = ref('')
let todoList = ref([])
// Delete
let isDeleteModal = ref(false)
let indexOfDelete = ref(null)
// Update
let currentName = ref('')
let isCancelModal = ref(false)
let indexOfEdit = ref(null)

const createTodo = () => {
  if (todo.value.trim() !== '') {
    const newTodo = {
      modelValue: todo.value,
      isUpdate: false,
      isChecked: false,
    }
    todoList.value.push(newTodo);

    // 초기화
    todo.value = ''
  } else {
    console.log(todo.value);
    console.log('할 일을 작성하지 않음')
  }
}

// Delete
// const openDeleteModal = (i) => {
//   indexOfDelete.value = i;
//   isDeleteModal.value = true;
// }
const closeDeleteModal = () => {
  isDeleteModal.value = false;
}
const deleteTodo = () => {
  if (indexOfDelete.value !== null) {
    todoList.value = todoList.value.filter((_, index) => index !== indexOfDelete.value);

    // 초기화
    indexOfDelete.value = null;
    isDeleteModal.value = false;
  }
}

// Update
// const startUpdate = (todo, i) => {
//   todoList.value[i].isUpdate = true;
//   currentName.value = todo.name;
//   indexOfEdit.value = i;
// }
// const escEndUpdate = (todo) => {
//   if (currentName.value !== todo.name) {
//     isCancelModal.value = true
//   } else {
//     todoList.value[indexOfEdit.value].isUpdate = false;
//   }
// }
const closeEscModal = () => {
  isCancelModal.value = false;
}
const notUpdateTodo = () => {
  if (indexOfEdit.value !== null) {
    todoList.value[indexOfEdit.value].name = currentName.value;
    todoList.value[indexOfEdit.value].isUpdate = false;

    // 초기화
    currentName.value = '';
    isCancelModal.value = false;
    indexOfEdit.value = null;
  }
}
</script>

<style lang="scss">
.home {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;

  position: relative;
}

.container {
  min-width: 350px;
  min-height: 350px;
  width: 75%;
  border: 1px solid #00c4c4;
  border-radius: 5px;

  padding: 24px;
}

button {
  background-color: #fff;
  color: #00c4c4;

  border-radius: 5px;
  border: 1px solid #00c4c4;
  padding: 0 20px;

  &:hover {
    background-color: #00c4c4;
    color: #fff;

    transition-property: background-color, color;
    transition-duration: .3s;
  }

  &:not(:hover) {
    background-color: #fff;
    color: #00c4c4;

    transition-property: background-color, color;
    transition-duration: .3s;
  }

  &:active {
    background-color: #009393;
    color: #fff;
  }
}

input {
  outline: none;
  border: 2px solid #00c4c4;

  &:hover {
    border-radius: 5px;
    border: 2px solid #8c4201;
    transition-property: border;
    transition-duration: .3s;
  }

  &:not(:hover) {
    border-radius: 5px;
    border: 2px solid #00c4c4;
    transition-property: border;
    transition-duration: .3s;
  }

  &:focus {
    border-radius: 5px;
    border: 2px solid #8c4201;
  }
}

.modal-background {
  width: 100%;
  height: 100vh;

  position: absolute;

  display: flex;
  justify-content: center;
  align-items: center;

  background-color: rgba(255, 255, 255, 0.8);

  .modal-content {
    width: 250px;
    height: 250px;

    border: 1px solid #8c4201;
    border-radius: 5px;
    background-color: #fff;

    padding: 24px;

    display: flex;
    flex-direction: column;

    h2 {
      margin-bottom: 10px;
    }

    p {
      flex: 1;
      margin-top: 10px;
    }

    div:last-of-type {
      display: flex;
      justify-content: flex-end;

      button:first-of-type {
        margin-right: 10px;
      }
    }
  }
}

.title {
  margin-bottom: 10px;
}

.add-input-container {
  margin: 10px 0;
  display: flex;

  input {
    height: 40px;
    flex: 1;
    margin-right: 10px;
    padding: 0 10px;
  }
}

.todo-list {
  margin: 10px 0;

  li {
    height: 30px;
    margin-bottom: 10px;
    display: flex;
    align-items: center;
    justify-content: center;

    input {
      margin-right: 10px;
    }

    div:first-of-type {
      flex: 1;
      margin-right: 10px;

      input {
        width: 100%;
        height: 20px;
        font-size: 1rem;
      }
    }

    div:last-of-type {
      button:last-of-type {
        margin-left: 10px;
      }
    }
  }

  li:last-of-type {
    margin-bottom: 0;
  }
}

.isCompleted {
  text-decoration: line-through;
}
</style>
