<template>
  <!-- Esc modal component -->
  <div v-if='props.isCancelModal' class="modal-background">
    <div class="modal-content">
      <h2>수정 취소</h2>
      <hr />
      <p>정말로 수정 취소하시겠습니까?</p>
      <div>
        <button @click="$emit('closeEscClick')">아니요</button>
        <button @click="$emit('notUpdateTodo')">예</button>
      </div>
    </div>
  </div>
  <!-- Esc modal component -->
  <!-- <CancelModal @close-esc-click="closeEscModal" @not-update-todo="notUpdateTodo" /> -->
</template>
<script setup>
import { defineProps } from 'vue'

let props = defineProps({
  isCancelModal: {
    type: Boolean,
  }
})
</script>
<style lang="scss" scoped></style>