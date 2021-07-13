<template>
  <h1>
    Home Page
  </h1>
  <button @click="toIngredients">check ingredients</button>
</template>

<script>
export default {
  name: 'Home',
  methods: {
    toIngredients() {
      this.$emit('next');
    },
  },
};
</script>

<style>
</style>
