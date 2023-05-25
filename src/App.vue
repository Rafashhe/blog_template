<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "09/04/1992",
          content: "Olá mundo",
        },
        {
          title: "Meu segundo post",
          datetime: "26/05/2023",
          content: "Gostaram da apresentação?",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
      this.posts[id] = updatedPost;
    },
    removePost(id) {
      this.posts.splice(id, 1);
    },
  },
};
</script>
<!-- a forma de passar informações: pai-> filho = props / filho -> pai = eventos -->
<template>
  <header>
    <nav>
      <RouterLink class="router" to="/">Home</RouterLink>
      <RouterLink class="router" to="/create">Novo Post</RouterLink>
    </nav>

    <RouterView
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="removePost"
    />
    <!-- quando (@) evento (nomeGenérico) for emitido = ele recebe (=) a função (nomeGenérico)-->
  </header>
</template>

<style scoped>

nav {
  position: fixed;
  left: 10%;
  top: 0;
  height: 4em;
  width: 90%;

  background-color: black;
  border: 1px solid transparent;

  display: flex;
  align-items: center;
  justify-content: end;
}

.router {
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-weight: 600;
  font-size: larger;
  color: darkgoldenrod;


  padding-left: 2em;
  padding-right: 4em;
}

</style>
