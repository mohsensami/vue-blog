<template>
  <div v-if="loading" class="spinner-border" role="status">
    <span class="visually-hidden">Loading...</span>
  </div>

  <div v-else class="col-md-4">
    <UserCardViwe :user="user" />
  </div>
  <div class="col-md-8">
    <h4>Posts</h4>
    <hr>
    <ul v-for="post in posts">
      <li class="d-flex">
        <router-link
          :to="{ name: 'postId', params: { id: post.id } }"
          >{{ post.title }}</router-link
        >

      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";
import UserCardViwe from "../../components/users/CardView.vue";
import { useRoute } from "vue-router";

export default {
  components: {
    UserCardViwe,
  },
  setup() {
    const user = ref({});
    const posts = ref({});
    const loading = ref(true);
    const route = useRoute();

    function getUser() {
      axios
        .get(`https://jsonplaceholder.typicode.com/users/${route.params.id}`)
        .then(function (response) {
          user.value = response.data;
          loading.value = false;
        })
        .catch(function (error) {
          console.log(error);
        });
    }
    getUser();
    
    function getPosts() {
      axios
        .get(`https://jsonplaceholder.typicode.com/posts?userId=${route.params.id}`)
        .then(function (response) {
          posts.value = response.data;
          loading.value = false;
        })
        .catch(function (error) {
          console.log(error);
        });
    }
    getPosts();

    return { user, loading, posts };
  },
};
</script>

<style>
</style>
