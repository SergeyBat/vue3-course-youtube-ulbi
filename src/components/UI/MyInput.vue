<template>
  <input
    class="input"
    :value="modelValue"
    :type="type"
    @input="updateInput"
  >
</template>

<script>
  export default {
    name: 'my-input',
    props: {
      modelValue: [String, Number],
      type: [String],
    },
    methods: {
      updateInput(event) {
        this.$emit('update:modelValue', event.target.value)
      }
    }
  }
</script>

<style scoped>
  .input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
  }
</style>
