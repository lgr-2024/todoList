<template>
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
</template>
<script>
export default {
  name: 'DeleteModal',
  data() { 
    return {
      // Delete
      isDeleteModal: false,
      indexOfDelete: null,
    }
  },
  methods: {
    // Delete
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
  }
}
</script>
<style lang="">
  
</style>