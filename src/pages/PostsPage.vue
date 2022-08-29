<template>
  <div>
    <h1>Страница с постами</h1>
    <MyInput v-model="searchQuery" placeholder="Поиск.." />
    <div class="app__btns">
      <MyButton @click="showDialog"> Создать пост </MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions" />
    </div>

    <MyDialog v-model:show="dialogVisible">
      <PostForm @create="createPost" />
    </MyDialog>
    <PostList
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>
    <div ref="observer" class="observer"></div>
    <!-- <PostPagination
      @change-page="changePage"
      :page="page"
      :totalPages="totalPages"
    /> -->
  </div>
</template>

<script>
import axios from 'axios';
import PostList from '@/components/PostList';
import PostForm from '@/components/PostForm';
//import PostPagination from '@/components/PostPagination.vue';

export default {
  components: {
    PostForm,
    PostList,
    // PostPagination
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      modificatorValue: '',
      isPostsLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        { value: 'title', name: 'По названию' },
        { value: 'body', name: 'По содержимому' },
      ],
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
    // changePage(pageNumber) {
    //   this.page = pageNumber;
    // },
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get(
          'https://jsonplaceholder.typicode.com/posts',
          {
            params: {
              _page: this.page,
              _limit: this.limit,
            },
          }
        );
        this.totalPages = Math.ceil(
          response.headers['x-total-count'] / this.limit
        );
        this.posts = response.data;
      } catch (e) {
        alert('Ошибка! ');
      } finally {
        this.isPostsLoading = false;
      }
    },
    async loadMorePosts() {
      try {
        this.page += 1;
        const response = await axios.get(
          'https://jsonplaceholder.typicode.com/posts',
          {
            params: {
              _page: this.page,
              _limit: this.limit,
            },
          }
        );
        this.totalPages = Math.ceil(
          response.headers['x-total-count'] / this.limit
        );
        this.posts = [...this.posts, ...response.data];
      } catch (e) {
        alert('Ошибка! ');
      }
    },
  },
  mounted() {
    this.fetchPosts();
    const options = {
      rootMargin: '0px',
      threshold: 1.0,
    };
    const callback = (entries, observer) => {
      if (entries[0].isIntersecting && this.page < this.totalPages) {
        this.loadMorePosts();
      }
    };
    const observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer);
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) =>
        post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
      );
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  watch: {
    // page() {
    //   this.fetchPosts();
    // }
    // selectedSort(newValue) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[newValue]?.localeCompare(post2[newValue]);
    //   });
    // },
  },
};
</script>

<style>
.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}

.observer {
  height: 30px;
  /* background-color: green; */
}
</style>
