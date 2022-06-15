<template>
  <div>
    <router-link class="btn btn-dark" :to="{ name: 'createPost' }">
      Create Post
    </router-link>
  </div>
  <div v-if="loading" class="spinner-border" role="status">
    <span class="visually-hidden">Loading...</span>
  </div>

  <div v-else class="col-md-3" v-for="post in posts" :key="post.id">
    <div class="card" style="width: 18rem">
      <img
        :src="`https://picsum.photos/id/${post.id}/300/200`"
        class="card-img-top"
        :alt="post.title"
      />
      <div class="card-body">
        <h5 class="card-title">
          {{ post.title }}
        </h5>
        <p class="card-text">{{ post.body }}</p>
        <router-link
          :to="{ name: 'postId', params: { id: post.id } }"
          class="btn btn-sm btn-primary"
          >See more</router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";

export default {
  setup() {
    const posts = ref([]);
    const loading = ref(true);

    function getPosts() {
      axios
        .get("https://jsonplaceholder.typicode.com/posts")
        .then(function (response) {
          posts.value = response.data;
          loading.value = false;
        })
        .catch(function (error) {
          console.log(error);
        });
    }

    getPosts();

    return { posts, loading };
  },
};
</script>

<style>
</style>