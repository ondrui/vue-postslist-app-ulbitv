<template>
  <div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> JavaScript универсальный язык программирования</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> JavaScript универсальный язык программирования</div>
    </div>
    <div class="post">
      <div><strong>Название:</strong> Пост о JavaScript</div>
      <div><strong>Описание:</strong> JavaScript универсальный язык программирования</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        likes: 0,
        dislikes: 0,
      }
    },
    methods: {
      addLikes() {
        this.likes += 1;
      },
      addDislike() {
        this.dislikes += 1;
      }
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
