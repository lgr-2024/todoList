<template>
  <input :value="value" @input="$emit('input', $event.target.value)" :type='type' :placeholder='placeholder' />
</template>
<script setup>

</script>
<script>
export default {
  name: 'TodoInput',
  props: {
    modelValue: {
      type: String,
      required: true
    },
    type: {
      type: String,
      default: 'text' // 'number', 'email'
    },
    placeholder: {
      type: String,
      default: '할 일을 작성해주세요.'
    },
  },
}
</script>

<style lang="scss" scoped>
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
</style>