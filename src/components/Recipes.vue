<template>
  <div class="container mt-5">
    <div class="row justify-content-md-center">
      <div class="col align-self-center">
        <h1>Your recipes</h1>
      </div>
    </div>
    <div class="row">
      <div
        v-for="recipe in recipeList"
        :key="recipe"
        class="card col-3"
        style="width: 18rem"
      >
        <div class="card-body">
          <h2>{{ recipe.title }}</h2>
        </div>
        <ul class="list-group">
          <li
            v-for="item in recipe.ingredients"
            :key="item"
            class="list-group-item"
          >
            -{{ item }}
          </li>
        </ul>
      </div>
    </div>
    <button type="button" class="btn btn-primary" @click="back">
      back to home
    </button>
  </div>
</template>

<script>
export default {
  name: 'Recipes',
  props: ['recipeList'],
  methods: {
    back() {
      this.$emit('switchPage', 'Home');
    },
  },
};
</script>

<style>
.card {
  margin: 10px;
}
</style>
