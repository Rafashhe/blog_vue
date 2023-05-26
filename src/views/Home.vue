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
    placeholder="      &#128269    Procure pelo título do post..."
  />

  <div id="lista-posts">
    <div class="post" v-for="post in filteredPosts" :key="post.key">
      <div class="flex">
        <RouterLink :to="`/detail/${getPostId(post.title)}`">
          <h3 class="flex nome">
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
      <h4 class="flex dia" >{{ post.datetime }}</h4>
      <p class="flex postagem" >{{ post.content }}</p>
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
.busca {
  position: fixed;
  top: 1.5%;
  left: 3%;
  
  height: 5%;
  width: 17%;
  padding: 0px 7px;
  
  border: none;
  border-radius: 6px;
  outline: none;
  background-color: transparent;
  box-shadow: 3px 3px 10px rgba(0,0,0,1),
  -1px -1px 6px rgba(255, 255, 255, 0.4);

  font-size: 15px;
  transition: 0.3s;
}

.busca:focus {
  box-shadow: 3px 3px 10px rgba(0,0,0,1),
  -1px -1px 6px rgba(255, 255, 255, 0.4),
  inset 3px 3px 10px rgba(0,0,0,1),
  inset -1px -1px 6px rgba(255, 255, 255, 0.4);
}

</style>