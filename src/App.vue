<script>
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "18/5/2023",
          content: "Olá mundo",
        },
        {
          title: "Meu segundo post",
          datetime: "15/5/2023",
          content: "Aniversário do Lucas",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
      this.posts [id].updatedPost;
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
    </nav>

    <RouterView :posts="posts" @create-post="addPost" @edit-post="updatePost" />
    <!-- quando (@) evento (nomeGenérico) for emitido = ele recebe (=) a função (nomeGenérico)-->
  </header>
</template>

<style scoped></style>
