<template>
  <div>
    <div class="post" v-bind:key="post.id" v-for="post in posts">
      <div><strong>Название:</strong> {{ post.title }}</div>
      <div><strong>Описание:</strong> {{ post.body }}</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        posts: [
          {id: 1, title: 'JavaScript 1', body: 'Описание поста 1'},
          {id: 2, title: 'JavaScript 2', body: 'Описание поста 2'},
          {id: 3, title: 'JavaScript 3', body: 'Описание поста 3'},
          {id: 4, title: 'JavaScript 4', body: 'Описание поста 4'},
        ]
      }
    },
    methods: {

    }
  }
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
  }

</style>
