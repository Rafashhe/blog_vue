<script>
import { RouterLink, RouterView } from "vue-router";
import "@/assets/base.css";

export default {
  data() {
    return {
      posts: [
        {
          title: "Meu primeiro post",
          datetime: "09/04/1992",
          content: "Olá mundo",
        },
        {
          title: "High School Life",
          datetime: "18/12/2009",
          content: "Escutando Evanescence e fingindo que não sou EMO",
        },
        {
          title: "Desesperos de uma universitária",
          datetime: "25/02/2016",
          content: "Eles disseram que seria divertido... E eu acreditei.",
        },
        {
          title: "New year, old me",
          datetime: "26/05/2023",
          content: "Gostaram da apresentação?",
        },
      ],
    };
  },
  methods: {
    addPost(newPost) {
      this.posts.push(newPost);
    },
    updatePost(updatedPost, id) {
      this.posts[id] = updatedPost;
    },
    removePost(id) {
      this.posts.splice(id, 1);
    },
  },
};
</script>
<!-- a forma de passar informações: pai-> filho = props / filho -> pai = eventos -->
<template>
  <header>
    <nav>
      <RouterLink class="router" to="/">Home</RouterLink>
      <RouterLink class="router" to="/create">Novo Post</RouterLink>
    </nav>

    <RouterView
      :posts="posts"
      @create-post="addPost"
      @edit-post="updatePost"
      @delete-post="removePost"
    />
    <!-- quando (@) evento (nomeGenérico) for emitido = ele recebe (=) a função (nomeGenérico)-->
  </header>
</template>

<style scoped>
nav {
  position: fixed;
  top: 0;
  left: 0;
  height: 8%;
  width: 100%;

  display: flex;
  align-items: center;
  justify-content: end;
  padding-right: 8rem;
  gap: 8rem;
  /* background-color: #5598b47e; */
}
.router {
  color: #fff !important;
  font-weight: bold;
  font-size: 2.6ch;
  text-transform: uppercase;
  
  transition: background-color 0.25s;
}
.router:hover {
  background-color: #e35884a9;
  border: 10px solid transparent;
  border-radius: 1em;
}
</style>
