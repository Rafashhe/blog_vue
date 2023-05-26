<script>
export default {
    props: {
        post: Object,
        id: String,
    },
    data() {
    return {
      formData: {
        title: this.post?.title || "",
        content: this.post?.content || "",
      },
      isEditing: Boolean (this.post),
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
      }/${now.getFullYear()} - ${now.getHours()}:${now.getMinutes()}`;

      const postData = {
        title: this.formData.title,
        content: this.formData.content,
        datetime: dataDaPostagem,
      };

      if (this.isEditing) {
        this.$emit("edit-post", postData, this.id);
      } else {
        this.$emit("create-post", postData);
      }

      this.$router.push("/");
    },
  },
};
</script>

<template>
  <form>
    <input class="insertBlog" v-model="formData.title" placeholder="Título" />

    <textarea
    class="insertBlog"
      v-model="formData.content"
      placeholder="Escreva seu post aqui..."
      id="textao"
      cols="30"
      rows="10"
    ></textarea>

    <button class="submit" type="button" @click="handleCreatePost">Postar</button>
  </form>

</template>


