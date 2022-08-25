<template>
  <div class="app">
    <h1>Страница с постами</h1>
    <div class="app__btns">
      <MyButton
        @click="showDialog"
      >
      Создать пост
    </MyButton>
    <MySelect
      v-model="selectedSort"
      :options="sortOptions"
    />
    </div>

    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost" />
    </MyDialog>
    <PostList
      :posts="sortedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>
import axios from 'axios';
import PostList from '@/components/PostList';
import PostForm from '@/components/PostForm';

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      modificatorValue: '',
      isPostsLoading: false,
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'По названию'},
        {value: 'body', name: 'По содержимому'}
      ]
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
      document.body.style.overflow = '';
    },
    removePost(post) {
      //this.posts = this.posts.filter(p => p.id !== post.id)
      this.posts.splice(this.posts.indexOf(post), 1);
    },
    showDialog() {
      document.body.style.overflow = 'hidden';
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
        this.posts = response.data;
      } catch (e) {
        alert('Ошибка! ');
      } finally {
        this.isPostsLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
    }
  },
  watch: {
    // selectedSort(newValue) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[newValue]?.localeCompare(post2[newValue]);
    //   });
    // },

  }
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

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>
