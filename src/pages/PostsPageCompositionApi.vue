<template>
  <div>
    <h1>Страница с постами</h1>
    <MyInput v-focus v-model="searchQuery" placeholder="Поиск.." />
    <div class="app__btns">
      <MyButton > Создать пост </MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions" />
    </div>

    <MyDialog v-model:show="dialogVisible">
      <PostForm />
    </MyDialog>
    <PostList
      :posts="sortedAndSearchedPosts"
      v-if="!isPostsLoading"
    />
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>
  import { ref } from "vue";
import axios from 'axios';
import PostList from '@/components/PostList';
import PostForm from '@/components/PostForm';
import usePosts from '@/hooks/usePosts';
import useSortedPosts from '@/hooks/useSortedPosts';
import useSortedAndSearchedPosts from '@/hooks/useSortedAndSearchedPosts';

export default {
  components: {
    PostForm,
    PostList,
    // PostPagination
  },
  data() {
    return {
      dialogVisible: false,
      sortOptions: [
        { value: 'title', name: 'По названию' },
        { value: 'body', name: 'По содержимому' },
      ],
    };
  },
  setup(props) {
    const {posts, isPostsLoading, totalPages} = usePosts(10);
    const {selectedSort, sortedPosts} = useSortedPosts(posts);
    const {searchQuery, sortedAndSearchedPosts} = useSortedAndSearchedPosts(sortedPosts);

    return {
      posts,
      isPostsLoading,
      totalPages,
      selectedSort,
      sortedPosts,
      searchQuery,
      sortedAndSearchedPosts,
    }
  }
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
