<template>
  <div class="home">
    <div class="container">
      <h1 class="title">Todo List</h1>
      <hr />
      <div class="add-input-container">
        <input
          v-model='todo'
          placeholder='할 일을 작성해주세요.'
          @keydown.enter="createTodo"
        />
        <!-- <todo-input
          :value="todo"
          v-on:input="update"
        /> -->
        <button type="button" @click="createTodo">추가</button>
        <!-- <todo-button @click="createTodo">추가2</todo-button> -->
      </div>
      <hr />
      <ul class="todo-list">
        <li v-for='(todo, index) in todoList' :key='index'>
          <input type='checkbox' v-model='todo.isChecked' />
          <div>
            <span
              v-if="!todo.isUpdate"
              :class='{ isCompleted: todo.isChecked }'
            >
              {{ todo.name }}
            </span>
            <input
              v-else
              v-model='todo.name'
              type="text"
              placeholder="할 일을 작성해주세요."
              @keydown.esc="escEndUpdate(todo, index)"
              @keydown.enter="todo.isUpdate = false"
            />
          </div>
          <div>
            <button v-if='!todo.isUpdate' type="button" @click="startUpdate(todo, index)">수정</button>
            <button v-else type="button" @click="todo.isUpdate = false">완료</button>
            <button type="button" @click="openDeleteModal(index)">삭제</button>
          </div>
        </li>
      </ul>
    </div>

    <!-- delete modal component -->
    <div v-if='isDeleteModal' class="modal-background">
      <div class="modal-content">
        <h2>삭제</h2>
        <hr />
        <p>정말로 삭제하시겠습니까?</p>
        <div>
          <button @click="closeDeleteModal">아니요</button>
          <button @click="deleteTodo">예</button>
        </div>
      </div>
    </div>
    <!-- delete modal component -->

    <!-- Esc modal component -->
    <div v-if='isCancelModal' class="modal-background">
      <div class="modal-content">
        <h2>수정 취소</h2>
        <hr />
        <p>정말로 수정 취소하시겠습니까?</p>
        <div>
          <button @click="closeEscModal">아니요</button>
          <button @click="notUpdateTodo">예</button>
        </div>
      </div>
    </div>
    <!-- Esc modal component -->
</div>
</template>

<script>
// import TodoInput from '@/components/common/TodoInput.vue'
// import TodoButton from '@/components/common/TodoButton.vue'

export default {
  name: 'TodoList',
  // components: {
  //   TodoInput,
  //   TodoButton,
  // },
  data() {
    return {
      todo: '',
      todoList: [],
      // Delete
      isDeleteModal: false,
      indexOfDelete: null,
      // Update
      currentName: '',
      isCancelModal: false,
      indexOfEdit: null,
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
      } else { 
        console.log(this.todo);
        console.log('할 일을 작성하지 않음')
      }
    },
    // Delete
    openDeleteModal(i) {
      this.indexOfDelete = i;
      this.isDeleteModal = true;
    },
    closeDeleteModal() {
      this.isDeleteModal = false;
    },
    deleteTodo() {
      if (this.indexOfDelete !== null) {
        this.todoList = this.todoList.filter((_, index) => index !== this.indexOfDelete);

        // 초기화
        this.indexOfDelete = null;
        this.isDeleteModal = false;
      }
    },
    startUpdate(todo, i) {
      this.todoList[i].isUpdate = true;
      this.currentName = todo.name;
      this.indexOfEdit = i;
    },
    escEndUpdate(todo) { 
      if (this.currentName !== todo.name) {
        this.isCancelModal = true
      } else {
        this.todoList[this.indexOfEdit].isUpdate = false;
      }
    },
    closeEscModal() { 
      this.isCancelModal = false;
    },
    notUpdateTodo() {
      if (this.indexOfEdit !== null) {
        this.todoList[this.indexOfEdit].name = this.currentName;
        this.todoList[this.indexOfEdit].isUpdate = false;

        // 초기화
        this.currentName = '';
        this.isCancelModal = false;
        this.indexOfEdit = null;
      }
    }
  }
}
</script>

<style lang="scss" scoped>
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
