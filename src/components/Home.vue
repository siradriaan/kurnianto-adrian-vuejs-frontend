<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-6 h-50">
        <div class="container">
          <div class="row">
            <div class="col-12">
                <h1>Recipe suggestion app</h1>
                <h6>This is a recipe suggestion app you can choose the following ingredients</h6>
                <div class="row">
                  <label class="col-4">recipe plan:</label>
                  <input class ="col-4" type="date" v-model="date" @change="clearChosen"/>
                  <p>ingredients: ( {{chosen.join(',')}} )</p>
                </div>
            </div>
          </div>
          <div class="row">
            <button
              type="button"
              class="btn btn-primary"
              @click="toRecipe">check recipe
            </button>
          </div>
        </div>
      </div>
      <div class="ingredient col-6 overflow-scroll">
        <ul class="list-group ">
          <li class="list-group-item "
          v-for="ingredient in availabilities"
          :key="ingredient">
            <input
              class="form-check-input me-1"
              type="checkbox"
              v-if="ingredient.disabled == false"
              :id="'ingredient_' + ingredient.title"
              :value="ingredient.title"
              v-model="chosen"
            />
            <label>{{ingredient.title}}</label>
            <p> best-before: {{ingredient['use-by']}}</p>
          </li>
        </ul>
      </div>
    </div>
  </div>
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
      }).then(async (response) => {
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
.row {
  padding: 10px;
}
.ingredient {
  height: 500px
}

</style>
