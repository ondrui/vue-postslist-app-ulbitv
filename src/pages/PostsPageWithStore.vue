<template>
  <div>
    <h1>{{ $store.state.post.limit }}</h1>
    <!-- <h1>Страница с постами</h1>
    <MyInput
      v-focus
      v-model="searchQuery"
      placeholder="Поиск.."
    />
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
    <div v-else>Идет загрузка...</div> -->
    <!-- <div v-intersection="loadMorePosts" class="observer"></div> -->
    <!-- <PostPagination
      @change-page="changePage"
      :page="page"
      :totalPages="totalPages"
    /> -->
  </div>
</template>

<script>
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
  },
  mounted() {
    //this.fetchPosts();
    // const options = {
    //   rootMargin: '0px',
    //   threshold: 1.0,
    // };
    // const callback = (entries, observer) => {
    //   if (entries[0].isIntersecting && this.page < this.totalPages) {
    //     this.loadMorePosts();
    //   }
    // };
    // const observer = new IntersectionObserver(callback, options);
    // observer.observe(this.$refs.observer);
  },
  computed: {

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
