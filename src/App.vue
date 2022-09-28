<template>
  <div class="app">
    <form @submit.prevent>
      <h4>Создание поста</h4>
      <input v-bind:value="title"
             @input="title = $event.target.value"
             class="input"
             type="text"
             placeholder="Название поста"
      >
      <input v-bind:value="body"
             @input="body = $event.target.value"
             class="input"
             type="text"
             placeholder="Описание поста"
      >
      <button
          class="my-button"
          @click="createPost"
      > Cоздать
      </button>
    </form>

    <div class="post" v-for="post in posts">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [
        {id: 1, title: 'JavaScri pt', body: 'Описание поста'},
        {id: 2, title: 'JavaScript', body: 'Описание поста'},
        {id: 3, title: 'JavaScript', body: 'Описание поста'},
        {id: 4, title: 'JavaScript', body: 'Описание поста'},
      ],
      title: '',
      body: ''
    }
  },
  methods: {
    createPost() {
      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body
      }
      this.posts.push(newPost)
      this.title = '';
      this.body = '';
    },
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

form {
  display: flex;
  flex-direction: column;
}

.post {
  margin: 15px;
  padding: 15px;
  border: 3px solid cyan;
}

.input {
  width: 100%;
  padding: 10px 15px;
  border: 3px solid cyan;
  margin-top: 15px;
}

.app {
  padding: 20px;
}

.my-button {
  border: 2px solid cyan;
  background: none;
  padding: 10px 15px;
  margin-top: 15px;
  align-self: flex-end;
}
</style>