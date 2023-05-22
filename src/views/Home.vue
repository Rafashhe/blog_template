<script>
import { RouterLink } from "vue-router";

// componentes dependem de uma informação do pai (app). O props "posts" está sendo definido no pai (app), aqui seria uma "cópia"
export default {
  props: {
    posts: Array,
  },

  data() {
    return {
      search: "",
      showModal: false,
      selectedPost: null,
      // diferença entre nulo e indefinido, nulo alguém já determinou, indefinido não existe.
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
  methods: {
    // serve para manipular o data através de variáves
    getPostId(title) {
      // passa pela lista de posts (não filtrada)
      for (const index in this.posts) {
        // acessa o post na posição index na lista de posts
        const post = this.posts[index];

        // verifica se o título do post atual é igual ao título buscado
        if (post.title === title) return index;
      }
    },
    deletePost() {
      const id = this.getPostId(this.selectedPost.title);
      this.$emit("delete-post", id);
      this.setupModal(); // sem id porque eu só quero a função de abrir e fechar o modal
    },
    setupModal(id) {
      this.showModal = !this.showModal;

      if (id) {
        this.selectedPost = this.posts[id];
        return;
        // return neste caso, encerra a função
      }
      this.selectedPost = null;
    },
  },
};
</script>

<template>
  <input v-model="search" placeholder="Procure pelo título do post..." />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.key">
      <div class="flex">
        <RouterLink :to="`/detail/${getPostId(post.title)}`">
          <h3>
            <!-- interface declarativa, sempre vem do data ou de um método. Métodos são funções -->
            {{ post.title }}
          </h3>
        </RouterLink>
        <RouterLink :to="`/edit/${getPostId(post.title)}`">
          <span class="material-symbols-outlined">edit</span>
        </RouterLink>
        <span
          class="material-symbols-outlined"
          @click="setupModal(getPostId(post.title))"
          >delete</span
        >
      </div>
      <h4>{{ post.datetime }}</h4>
      <p>{{ post.content }}</p>
    </div>
  </div>

  <div class="modal" v-show="showModal">
    <div class="modal-content">
      <h3>Deletar Post</h3>
      <p>Tem certeza que deseja deletar o '{{ selectedPost?.title }}'?</p>
      <p>Esta ação é irreversivel</p>

      <div class="modal-actions">
        <button class="bg-sucess" @click="deletePost">Confirmar</button>
        <button class="bg-error" @click="setupModal">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

textarea {
    resize: none;
    outline: none;
    border: none;
    width: 80%;
}

</style>