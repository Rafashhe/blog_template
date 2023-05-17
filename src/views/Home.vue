<script>
import { RouterLink, RouterView } from "vue-router";
import posts from '../App.vue'

export default {
    props: {
        posts: Array,
    },
};
</script>

<template>
<input v-model="search" placeholder="Procure pelo título do post..." />

<div id="lista-posts">
  <div class="post" v-for="post in filteredPosts" :key="post.key">
    <h3>{{ post.title }}</h3>
    <h4>{{ post.datetime }}</h4>
    <p>{{ post.content }}</p>
  </div>
</div>

<RouterView />
</template>
