<template>
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
</template>
<script>
export default {
  name: 'CancelModal',
  data() { 
    return {
      // Update
      currentName: '',
      isCancelModal: false,
      indexOfEdit: null,
    }
  },
  methods: {
    // Update
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
  
</style>