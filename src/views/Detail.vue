<script>
export default {
  props: {
    posts: Array,
  },
  data() {
    // acessa o parâmetro id uma única vez
    const id = this.$route.params.id;

    return {
      // expondo a variável id para ser acessível no template
      id: id,
      post: this.posts[id],
    };
  },
};
</script>
<!-- o "this" eu só coloco no script-->
<template>
  <main>
    <h2 class="box title">
      {{ post.title }}
    </h2>
    <h4 class="box dia-post">{{ post.datetime }}</h4>
    <textarea class="detailedPost" readonly :value="post.content"></textarea>
  </main>
</template>

