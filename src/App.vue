<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
  },
};
</script>
<!-- a forma de passar informações: pai-> filho = props / filho -> pai = eventos -->
<template>
  <header>
    <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/create">Novo Post</RouterLink>
      <RouterLink to="/detail/:id">Arquivos</RouterLink>
      <RouterLink to="/edit/:id">Edição</RouterLink>
    </nav>

    <RouterView :posts="posts" @create-post="addPost" />
    <!-- quando (@) evento (nomeGenérico) = função (nomeGenérico)-->
  </header>
</template>

<style scoped></style>
