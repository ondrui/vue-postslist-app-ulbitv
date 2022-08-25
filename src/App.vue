<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <input type="text" v-model.trim="modificatorValue">
    <MyButton
      @click="showDialog"
      style="margin: 15px 0;"
    >
      Создать пост
    </MyButton>
    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost" />
    </MyDialog>

    <PostList :posts="posts" @remove="removePost" />
  </div>
</template>

<script>
import PostList from '@/components/PostList';
import PostForm from '@/components/PostForm';

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [
        { id: 1, title: 'JavaScript 1', body: 'Описание поста 1' },
        { id: 2, title: 'JavaScript 2', body: 'Описание поста 2' },
        { id: 3, title: 'JavaScript 3', body: 'Описание поста 3' },
        { id: 4, title: 'JavaScript 4', body: 'Описание поста 4' },
      ],
      dialogVisible: false,
      modificatorValue: '',
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
      document.body.style.overflow = "";
    },
    removePost(post) {
      //this.posts = this.posts.filter(p => p.id !== post.id)
      this.posts.splice(this.posts.indexOf(post), 1);
    },
    showDialog() {
      document.body.style.overflow = "hidden";
      this.dialogVisible = true;
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
