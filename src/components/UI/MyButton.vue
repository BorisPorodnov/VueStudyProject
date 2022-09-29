<template>
  <button class="my-button">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'my-button'
}
</script>

<style scoped>
.my-button {
  border: 2px solid cyan;
  background: none;
  padding: 10px 15px;
}
</style>