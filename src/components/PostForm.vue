<template>
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
      > Cоздать
      </button>
    </form>
</template>

<script>
export default {

}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}



.input {
  width: 100%;
  padding: 10px 15px;
  border: 3px solid cyan;
  margin-top: 15px;
}

.my-button {
  border: 2px solid cyan;
  background: none;
  padding: 10px 15px;
  margin-top: 15px;
  align-self: flex-end;
}
</style>