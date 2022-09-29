<template>
  <div>

    <div class="post" v-for="post in posts">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {

  props:{
    posts:{
      type: Array,
      required:true
    }
  }
}
</script>

<style scoped>
.post {
  margin: 15px;
  padding: 15px;
  border: 3px solid cyan;
}
</style>