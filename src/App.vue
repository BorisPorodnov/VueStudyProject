<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <my-input
        v-model="searchQuery"
        placeholder="Поиск...."
    />
    <div class="app_btn">
      <my-button
          @click="showDialog"
      >
        Создать пост
      </my-button>
      <my-select
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>

    <my-dialog v-model:show="dialogVisible">
      <post-form
          @create="createPost"
      />
    </my-dialog>
    <post-list
        :posts="sortedAndSearchPosts"
        @create="createPost"
        @remove="removePost"
        v-if="!isPostLoading"
    />
    <div v-else>Идет загрузка....</div>
    <div class="page__wrapper">
      <div v-for="pageNumber in totalPages"
           :key="pageNumber"
           class="page"
           :class="{
             'current-page': page === pageNumber
           }"
      >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<script>

import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from 'axios';

export default {
  components: {
    PostForm, PostList
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По содержимому'},
      ]
    }
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts =
          this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        });
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
        this.posts = response.data;
      } catch (e) {
        alert('ошибка')
      } finally {
        this.isPostLoading = false;
      }
    }
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) =>
          post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
    },
    sortedAndSearchPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}

.app_btn {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.page__wrapper {
  display: flex; /*для того что бы страницы выстроились в один ряд*/
  margin-top: 15px; /*отлепляем от самих постов*/
}

.page {
  border: 1px solid black; /*рамка*/
  padding: 10px; /*внутренние отступы*/
}

.current-page {
  border: 15px solid teal; /*рамка*/
}
</style>