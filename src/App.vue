<template>
  <div>
    <Home v-if="currentPage == 1"
      @next="nextPage"
    />
    <Ingredients v-else-if="currentPage == 2"
      @back="prevPage"
      @next="nextPage"
    />
    <Recipes v-else-if="currentPage == 3"
      @back="prevPage"
    />
  </div>
</template>

<script>
import Home from './components/Home.vue';
import Ingredients from './components/Ingredients.vue';
import Recipes from './components/Recipes.vue';

export default {
  name: 'app',
  components: {
    Home,
    Ingredients,
    Recipes,
  },
  data() {
    return {
      currentPage: 1,
    };
  },
  methods: {
    nextPage() {
      this.currentPage += 1;
    },
    prevPage() {
      this.currentPage -= 1;
    },
  },
};
</script>

<style>
</style>
