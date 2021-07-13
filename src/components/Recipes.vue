<template>
  <h1>
    Recipe Page
  </h1>
  <button  @click="back">back to Home</button>
</template>

<script>

export default {
  name: 'Recipes',
  methods: {
    back() {
      this.$emit('switchPage', -1);
    },
  },
};
</script>

<style>
</style>
