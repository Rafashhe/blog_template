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
  <input
    class="busca"
    v-model="search"
    placeholder="Procure pelo título do post..."
  />

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
      <p><strong>Esta ação é irreversivel</strong></p>

      <div class="modal-actions">
        <button class="bg-sucess" @click="deletePost">Confirmar</button>
        <button class="bg-error" @click="setupModal">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<style scoped>

.flex {
  background-color: aqua;
}

textarea {
  resize: none;
  outline: none;
  border: none;
  width: 80%;
}

/* .x {
  display: grid;
  word-wrap: break-word;
  place-items: center;
}

.box {
  min-width: 50%;
  max-width: 95%;
  margin-bottom: 10px;

  background-color: rgba(216, 221, 216, 0.541);
  cursor: pointer;

  border-radius: 0.3rem;
  outline: 0.3rem;
  outline-style: outset;
  outline-color: darkgoldenrod;
}

.box:hover {
  background-color: rgba(216, 221, 220, 0.877);
  border-radius: 0.7rem;
  box-shadow: inset 2px 5px 7px rgb(68, 66, 43);
  outline-color: darkgoldenrod;
}

.title {
  text-align: center;
  font-family: "RocherColor";
  font-size: 30px;
  word-wrap: break-word;

  padding-top: 0.7em;
  padding-inline: 0.7em;
}
.dia-post {
  text-align: right;
  font-weight: 600;
  font-size: medium;
  padding-top: 0.3em;
  padding-inline: 0.5em;
}

p {
  margin-top: 0;
  margin-bottom: 10px;
  padding: 1rem;

  min-width: 48%;
  max-width: 95%;

  background: linear-gradient(#fff, #fff) padding-box,
              linear-gradient(157deg, #00ff75, #3700ff) border-box;
  border: 5px solid transparent;
  border-radius: 0.5rem;

  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-weight: 600;
  color: rgb(24, 161, 161);
  letter-spacing: 1px;
} */


</style>
