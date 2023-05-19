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
/* .x {
box-sizing: content-box;
border: 5px solid;
box-shadow: 0 0 0 1px red, 0 2px 5px rgba(255, 255, 255, 0.3) outset;
} */

h3 {
  text-align: center;
  font-family: 'RocherColor';
  font-size: 30px;
  word-wrap: break-word;

  padding: 10px;
  border: 1px solid transparent;
  border-radius: 0.5rem;
  outline-style: outset;
  outline-color: darkgoldenrod;
}

h4 {
  background-color: blue;
  text-align: right;
  font-weight: inherit;
}

p {
  background-color: #ffffff;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
  font-weight: 600;
  /* color: rgb(71, 47, 14); */
  color: rgb(24, 161, 161);
  letter-spacing: 1px;
  
  padding: 1rem;
  box-shadow: 0 15px 30px 0 rgba(0,0,0,0.11),
    0 5px 15px 0 rgba(0,0,0,0.08);
  
  border-radius: 0.5rem;
  
  border-left: 0 solid #00ff99;
  transition: border-left 300ms ease-in-out, padding-left 300ms ease-in-out;
}

p:hover {
  padding-left: 0.5rem;
  border-left: 0.5rem solid #00ff99;
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
