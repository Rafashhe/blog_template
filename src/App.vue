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
    };
  },
  methods: {
handleSubmit (event) {
  event.preventDefault();

  console.log(this.title, this.content)
}
  }

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
  

  <form action="">
    <input name="title">
    <textarea name="content" id="" cols="30" rows="10"></textarea>
    <button>Criar</button>
  </form>
  <!-- {{ posts[0]. title }} -->

  <RouterView />
</template>

<style scoped>

form{
  display: flex;
  flex-direction: column;
}

form > * {
margin: 1rem;
}

</style>
