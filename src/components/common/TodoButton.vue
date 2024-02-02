<template>
    <button
      type='button'
      @click='clickEvent'>
      추가2
    </button>
</template>

<script>
export default {
  name: 'TodoButton',
  methods: {
    clickEvent() {
      console.log('click')
      this.$emit('click')
    }
  }
}
</script>

<style lang="scss" scoped>
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
</style>