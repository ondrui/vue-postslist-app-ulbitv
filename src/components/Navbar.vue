<template>
  <div class="navbar">
    <div @click="$router.push('/')" style="padding: 20px">Vue 3</div>
    <div class="navbar__btns">
      <MyButton @click="$router.push('/posts')"> Посты </MyButton>
      <MyButton @click="$router.push('/about')" style="margin-left: 20px">
        О сайте
      </MyButton>
      <MyButton @click="$router.push('/store')" style="margin-left: 20px">
        store
      </MyButton>
      <MyButton @click="$router.push('/composition')" style="margin-left: 20px">
        Composition
      </MyButton>
      <MyButton @click="$router.push('#new-10')" style="margin-left: 20px">
        Post #10
      </MyButton>
      <MyButton @click="console" style="margin-left: 20px">
        $router
      </MyButton>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    console() {
      return console.log(this.$route)
    }
  }
};
</script>

<style scoped>
.navbar {
  position: fixed;
  width: 100%;
  top: 0;
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
