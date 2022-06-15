<template>
  <div class="card">
    <div class="card-header">
      <img
        :src="`https://i.pravatar.cc/400?img=${user.id}`"
        class="card-img-top"
        :alt="user.title"
      />
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">
        <router-link :to="{ name: 'userId', params: { id: user.id } }">{{
          user.name
        }}</router-link>
      </li>
      <li class="list-group-item">Username : {{ user.username }}</li>
      <li class="list-group-item">Email : {{ user.email }}</li>
      <li class="list-group-item">Phone : {{ user.phone }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    user: Object,
  },
};
</script>

<style>
</style>