<script>
import { RouterLink, RouterView } from "vue-router";


export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro Post",
          datetime: Date.now(),
          content: "Dear Diary",
        },
        {
          title: "Meu segundo Post",
          datetime: Date.now(),
          content: "Querido diário",
        },
      ],
      search: "",
    };
  },
  computed: {
    filteredPosts() {
      // se search estiver vazio, retorne a lista completa de posts
      if (!this.search) return this.posts;

      // lista filtrada é o nome genérico
      // se tiver qualquer coisa em search, faz o filtro
      const listaFiltrada = [];

      for (const post of this.posts) {
        if (post.title.includes(this.search)) {
          listaFiltrada.push(post);

          // operadores lógicos
        }
      }
      return listaFiltrada;
    },
  },
};
</script>

<template>

<header>
  
  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/create">Novo Post</RouterLink>
    <RouterLink to="/detail/:id">Arquivos</RouterLink>
    <RouterLink to="/edit/:id">Edição</RouterLink>
  </nav>

<RouterView />  

</header>
 
</template>

<style scoped></style>
