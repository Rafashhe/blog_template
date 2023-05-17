<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

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

h3 {
  text-align: center;
  width: 50%;
  font-family: 'RocherColor';
  font-size: 30px;
  padding: 10px;
  word-wrap: break-word;
  border: 1px solid transparent;
  box-shadow: 0 0 0 1px transparent, 0 2px 5px rgba(255, 255, 255, 0.3) outset;
}

h4 {
  background-color: blue;
  text-align: left;
  font-weight: inherit;
}

p {
  background-color: brown;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  letter-spacing: 1px;
  max-width: 60%;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 45%;
}

form > * {
  margin: 1rem;
  width: 90%;
}

input#título {
  border-radius: 7px;
  padding: 9px;
  background-color: #20212b;
  box-shadow: inset 2px 5px 7px rgb(0, 0, 0);
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-weight: bold;
  color: lightgray;
}

textarea#texto {
  border-radius: 17px;
  padding: 12px;
  background-color: #20212b;
  box-shadow: inset 2px 5px 10px rgb(0, 0, 0);
  color: lightgray;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

button {
  border-color: aqua;
  border-radius: 20px;
  width: 30%;
  padding: 12px;
  transition: 0.4s ease-in-out;
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
