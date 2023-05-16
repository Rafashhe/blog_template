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
  <div id="lista-posts">
    <div class="x" v-for="x in posts" :key="x.key">
      <h3>{{ x.title }}</h3>
      <h4>{{ x.datetime }}</h4>
      <p>{{ x.content }}</p>
    </div>
  </div>

  <form>
    <input v-model="formData.title" placeholder="Título" id="título" />

    <textarea
      name="content"
      :value="formData.content"
      placeholder="Escreva seu post aqui..."
      @keyup="handleInputChange"
      id="texto"
      cols="30"
      rows="10"
    ></textarea>

    <button type="button" @click="handleClick">Criar</button>
  </form>
  <!-- {{ posts[0]. title }} -->

  <RouterView />
</template>

<style scoped>
/* h3 {
  background-color: aquamarine;
}

h4 {
  background-color: blue;
}

p {
  background-color: brown;
} */

form {
  display: flex;
  flex-direction: column;
  width: 50%;
}

form > * {
  margin: 1rem;
}

input#título {
  border-radius: 7px;
  padding: 9px;
  background-color: #20212b;
  box-shadow: inset 2px 5px 7px rgb(0, 0, 0);
}

textarea#texto {
  border-radius: 17px;
  padding: 12px;
  background-color: #20212b;
  box-shadow: inset 2px 5px 10px rgb(0, 0, 0);
  
}

button {
  border-color: aqua;
  border-radius: 20px;
  width: 20em;
  padding: 0.9em;
  margin-left: 25em;
  transition: .4s ease-in-out;
  background: linear-gradient(163deg, #00642f 0%, #780ba3 100%);
  color: rgb(0, 255, 200);
  
  font-size: 0.9rem;
}

button:hover {
  border-color: #13034b;
  background: linear-gradient(163deg, #00ff75 0%, #3700ff 100%);
  color: rgb(0, 0, 0);
}

</style>
