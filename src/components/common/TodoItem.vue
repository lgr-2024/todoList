<template>
  <input type='checkbox' :isChecked="props.isChecked" @input="$emit('checkedClick', props.isChecked)" />
  <div>
    <span v-if="!props.isUpdate" :class='{ isCompleted: props.isChecked }'>
      {{ props.modelValue }}
    </span>
    <input v-else :value='props.modelValue' @input="handleInput" type="text" placeholder="할 일을 작성해주세요."
      @keydown.esc="$emit('escEndUpdate')" @keydown.enter="$emit('keydownEnter')" />
  </div>
  <div>
    <button v-if='!props.isUpdate' type="button" @click="$emit('startUpdateClick', props.todo, props.index)">수정</button>
    <button v-else type="button" @click="$emit('endUpdateClick')">완료</button>
    <button type="button" @click="$emit('deleteClick', props.index)">삭제</button>
  </div>
  <!-- <TodoItem :modelValue="todo.name" :isUpdate="todo.isUpdate" :isChecked="todo.isChecked" :index="index"
    @checked-click="todo.isChecked = !todo.isChecked" @escEndUpdate="escEndUpdate"
    @keydownEnter="todo.isUpdate = false" @startUpdateClick="startUpdate" @endUpdateClick="todo.isUpdate = false"
    @deleteClick="openDeleteModal" /> -->
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

let props = defineProps({
  modelValue: {
    type: String
  },
  todo: {
    type: Object
  },
  isUpdate: {
    type: Boolean,
  },
  isChecked: {
    type: Boolean,
  },
  index: {
    type: Number,
  }
})

const emit = defineEmits(["update:modelValue", "update:isUpdate", "update:isChecked"])

const handleInput = ($event) => {
  emit('update:modelValue', $event.target.value)
}
</script>

<style lang="scss" scoped>
.isCompleted {
  text-decoration: line-through;
}
</style>