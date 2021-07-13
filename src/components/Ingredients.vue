<template>
  <h1>
    Ingredients Page
  </h1>
  <button  @click="toHome">back to home</button>
  <button  @click="toRecipe">find recipe</button>
</template>

<script>
export default {
  name: 'Ingredients',
  methods: {
    toHome() {
      this.$emit('back');
    },
    toRecipe() {
      this.$emit('next');
    },
  },
};
</script>

<style>
</style>
