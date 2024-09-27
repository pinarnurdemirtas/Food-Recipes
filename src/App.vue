<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-4">Yemek Tarifleri</h1>

   
    <div class="mb-4 flex justify-between items-center">
  
      <SearchBar @search="searchMeals" />
      
      <div>
        <label for="mealType" class="mr-2">Yemek Türü:</label>
        <select v-model="selectedMealType" @change="filterMeals" id="mealType" class="border p-2 rounded">
          <option value="all">Hepsi</option>
          <option value="Chicken">Tavuk</option>
          <option value="Beef">Et</option>
          <option value="Seafood">Deniz Ürünleri</option>
        </select>
      </div>
    </div>

    <div class="grid grid-cols-3 gap-6">
    
      <MealCard v-for="recipe in filteredRecipes" :key="recipe.idMeal" :recipe="recipe" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue'; 
import MealCard from './components/MealCard.vue'; 

export default {
  components: {
    SearchBar, 
    MealCard   
  },
  data() {
    return {
      recipes: [],
      filteredRecipes: [],
      selectedMealType: 'all',
    };
  },
  mounted() {
    this.getMeals();
  },
  methods: {
    getMeals() {
      axios.get('https://www.themealdb.com/api/json/v1/1/search.php?s=')
        .then(response => {
          this.recipes = response.data.meals;
          this.filteredRecipes = this.recipes;
        });
    },
    filterMeals() {
      if (this.selectedMealType === 'all') {
        this.filteredRecipes = this.recipes;
      } else {
        this.filteredRecipes = this.recipes.filter(recipe =>
          recipe.strCategory === this.selectedMealType);
      }
    },
    searchMeals(searchQuery) {
      if (searchQuery) {
        this.filteredRecipes = this.recipes.filter(recipe =>
          recipe.strMeal.toLowerCase().includes(searchQuery.toLowerCase())
        );
      } else {
        this.filteredRecipes = this.recipes;
      }
    }
  }
};
</script>

<style scoped>
.grid {
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
}
</style>
