<template>
  <div class="navbar">
    <div
      @click="$router.push('/')"
      style="padding: 20px"
    >
      Vue 3
    </div>
    <div class="navbar__btns">
      <MyButton @click="$router.push('/posts')">Посты</MyButton>
      <MyButton
      @click="$router.push('/about')"
        style="margin-left: 20px"
      >
        О сайте
      </MyButton>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
  .navbar {
    height: 50px;
    background-color: rgb(168, 168, 168);
    box-shadow: 2px 2px 4px gray;
    display: flex;
    align-items: center;
    padding: 0 15px;
  }

  .navbar__btns {
    margin-left: auto;
  }
</style>
