<template>
  <form @submit.prevent>
    <h4>Создание поста</h4>
    <MyInput
      v-model="post.title"
      type="text"
      placeholder="Название"
      required
    />
    <MyInput
      v-model="post.body"
      type="text"
      placeholder="Описание"
      required
    />
    <MyButton class="btn_form" @click="createPost"> Создать </MyButton>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: '',
        body: '',
      },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post);
      this.post = {
        title: '',
        body: '',
      };
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}

.btn_form {
  align-self: flex-end;
  margin-top: 15px;
}
</style>
