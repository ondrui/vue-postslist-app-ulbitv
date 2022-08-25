<template>
  <div v-if="posts.length > 0">
    <h3>Список пользователей</h3>
    <PostItem
      :key="post.id"
      v-for="post in posts"
      :post="post"
      @remove="$emit('remove', post)"
    />
  </div>
  <h2 v-else style="color: red">
    Список постов пуст!
  </h2>
</template>

<script>
import PostItem from './PostItem.vue';
export default {
  components: {
    PostItem
  },
  emits:['remove'],
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  components: { PostItem },
};
</script>

<style scoped>
</style>
