<template>
  <div v-if="posts.length > 0">
    <h3>Список пользователей</h3>
    <TransitionGroup name="post-list">
      <PostItem
        :key="post.id"
        v-for="post in posts"
        :post="post"
        @remove="$emit('remove', post)"
      />
    </TransitionGroup>
  </div>
  <h2 v-else style="color: red">Список постов пуст!</h2>
</template>

<script>
import PostItem from './PostItem.vue';
export default {
  components: {
    PostItem,
  },
  emits: ['remove'],
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
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active ,
.post-list-move{
  transition: all 0.8s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
</style>
