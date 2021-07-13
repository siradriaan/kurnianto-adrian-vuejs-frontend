<template>
  <h1>
    Home Page
  </h1>
  <input type="date" v-model="date" @change="clearChosen"/>
    <div v-for="ingredient in availabilities" :key="ingredient">
      <input type="checkbox"
          v-if="ingredient.disabled == false"
          :id="'ingredient_' + ingredient.title"
          :value="ingredient.title"
          v-model="chosen"
          />
      <label>{{ ingredient.title }} : {{ ingredient['use-by'] }}</label>
    </div>
    {{chosen}}
    <button @click="toRecipe">check recipe</button>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Home',
  data() {
    return {
      ingredientList: [],
      date: new Date().toISOString().slice(0, 10),
      chosen: [],
    };
  },
  methods: {
    clearChosen() {
      this.chosen = [];
    },
    toRecipe() {
      this.$emit('fetch-recipe', this.chosen.join(','));
      this.$emit('switch-page', 'Recipe');
    },
    fetchIngredients() {
      axios({
        url: 'https://lb7u7svcm5.execute-api.ap-southeast-1.amazonaws.com/dev/ingredients',
        method: 'GET',
      })
        .then(async (response) => {
          this.ingredientList = response.data;
        });
    },
  },
  created() {
    this.fetchIngredients();
  },
  computed: {
    availabilities() {
      return this.ingredientList.map((e) => {
        if (new Date(e['use-by']) < new Date(this.date)) {
          return { ...e, disabled: true };
        }
        return { ...e, disabled: false };
      });
    },
  },
};
</script>

<style>
</style>
