<script>
export default {
    props: {
        post: Object,
    },
    data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
    };
  },
  methods: {
    handleCreatePost(event) {
      if (!this.formData.title) {
        alert("Preencha o título do post");
        return;
      }

      const now = new Date();

      const dataDaPostagem = `${now.getDate()}/${
        now.getMonth() + 1
      }/${now.getFullYear()}`;

      //   this.posts.push({
      //     title: this.formData.title,
      //     content: this.formData.content,
      //     datetime: dataDaPostagem,
      //   });

      const newPost = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      this.$emit("create-post", newPost);

      this.formData = {
        title: "",
        content: "",
      };

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <input v-model="formData.title" placeholder="Título" />

    <textarea
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      id=""
      cols="30"
      rows="10"
    ></textarea>

    <button type="button" @click="handleCreatePost">Criar</button>
  </form>
  <!-- {{ posts[0]. title }} -->
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
