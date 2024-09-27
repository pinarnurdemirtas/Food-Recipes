<template>
    <div class="card border rounded-lg p-4 shadow-md flex items-center">
      <img :src="recipe.strMealThumb" alt="Yemek Resmi" class="rounded-full w-32 h-32 object-cover mr-4" />
      <div>
        <h2 class="text-xl font-bold mb-2">{{ recipe.strMeal }}</h2>
        <p class="text-sm">{{ recipe.strInstructions.substring(0, 100) }}...</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['recipe']
  };
  </script>
  
  <style scoped>
  .card {
    transition: transform 0.2s ease-in-out;
  }
  .card:hover {
    transform: scale(1.05);
  }
  </style>
  