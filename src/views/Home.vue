<script>
import { RouterLink, RouterView } from "vue-router";
import posts from '../App.vue'

export default {
    props: {
        posts: Array,
    },
    
    data () {
      return {
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
