<template>
  <div>
    <Home v-if="currentPage == 'Home'"
      :ingredientList="ingredientList"
      @change-page="changeAvailability"
      @switch-page="switchPage"
    />
    <Recipes v-else-if="currentPage == 'Recipe'"
      @switch-page="switchPage"
    />
  </div>
</template>

<script>
import Home from './components/Home.vue';
import Recipes from './components/Recipes.vue';

export default {
  name: 'app',
  components: {
    Home,
    Recipes,
  },
  data() {
    return {
      currentPage: 'Home',
    };
  },
  methods: {
    switchPage(val) {
      this.currentPage += val;
    },
  },
};
</script>

<style>
</style>
