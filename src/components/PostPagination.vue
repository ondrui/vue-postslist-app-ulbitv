<template>
  <div class="page__wrapper">
    <div
      v-for="pageNumber in totalPages"
      :key="pageNumber"
      class="page"
      :class="{
        'current-page': page === pageNumber,
      }"
      @click="$emit('change-page', pageNumber)"
    >
      {{ pageNumber }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    page: Number,
    totalPages: Number
  }
};
</script>

<style scoped>
.page__wrapper {
  display: flex;
  margin-top: 15px;
  gap: 5px;
}

.page {
  border: 2px solid teal;
  padding: 10px;
  border-radius: 5px;
}

.current-page {
  border: 3px solid rgb(1, 62, 62);
  background-color: rgb(210, 207, 207);
  font-weight: bold;
}
</style>
