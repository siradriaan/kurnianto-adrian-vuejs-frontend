<template>
  <div>
    <Home v-if="currentPage == 'Home'"
      :ingredientList="ingredientList"
      @switch-page="switchPage"
      @fetch-recipe="fetchRecipe"
    />
    <Recipes v-else-if="currentPage == 'Recipe'"
      @switch-page="switchPage"
      :recipeList="recipeList"
    />
  </div>
</template>

<script>
import axios from 'axios';
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
      recipeList: [],
    };
  },
  methods: {
    switchPage(val) {
      this.currentPage = val;
    },
    fetchRecipe(value) {
      console.log(value);
      axios({
        url: `https://lb7u7svcm5.execute-api.ap-southeast-1.amazonaws.com/dev/recipes?ingredients${value}`,
        method: 'GET',
      })
        .then((response) => {
          this.recipeList = response.data;
          console.log(this.recipeList);
        });
    },
  },
};
</script>

<style>
</style>
