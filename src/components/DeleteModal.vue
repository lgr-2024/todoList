<template>
  <!-- delete modal component -->
  <div v-if='props.isDeleteModal' class="modal-background">
    <div class="modal-content">
      <h2>삭제</h2>
      <hr />
      <p>정말로 삭제하시겠습니까?</p>
      <div>
        <button @click="$emit('closeDeleteClick')">아니요</button>
        <button @click="$emit('deleteTodoClick')">예</button>
      </div>
    </div>
  </div>
  <!-- delete modal component -->
  <!-- <DeleteModal @close-delete-click="closeDeleteModal" @delete-todo-click="deleteTodo" /> -->
</template>

<script setup>
import { defineProps } from 'vue'

let props = defineProps({
  isDeleteModal: {
    type: Boolean,
  }
})
</script>
<style lang="scss"></style>