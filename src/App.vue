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
      <div class="box">
        <h3 class="title">{{ x.title }}</h3>
        <h2 class="dia-post">{{ x.datetime }}</h2>
      </div>
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
.x {
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
