<template>
  <h1>
    Recipe Page
  </h1>
  <button  @click="toIngredients">back to ingredients</button>
</template>

<script>

export default {
  name: 'Recipes',
  methods: {
    toIngredients() {
      this.$emit('back');
    },
  },
};
</script>

<style>
</style>
