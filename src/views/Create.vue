<script>
import { RouterLink, RouterView } from "vue-router";


export default {
  data() {
    return {
      formData: {
        title: "",
        content: "",
      },
    };
  },
  methods: {
    handleClick(event) {
      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      this.posts.push({
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      });

      this.formData = {
        title: "",
        content: "",
      };
    },

    handleInputChange(event) {
      const { name, value } = event.target;
      this.formData[name] = value;
    },
  },
};
</script>

<template>
  <form>
    <input v-model="formData.title" placeholder="Título" />

    <textarea
      name="content"
      :value="formData.content"
      placeholder="Escreva seu post aqui..."
      @keyup="handleInputChange"
      id=""
      cols="30"
      rows="10"
    ></textarea>

    <button type="button" @click="handleClick">Criar</button>
  </form>
  <!-- {{ posts[0]. title }} -->
  <RouterView />
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

form > * {
  margin: 1rem;
}
</style>
