<template>
<div class="p-8 pb-0 text-orange-500">
  <h1 class="text-4xl font-bold mb-4">Add Recipe</h1>
  <form @submit.prevent="submitForm" class="mt-8 flex flex-col gap-4 items-start">
      <div class="w-full">
        <label for="recipe-title" class="block mb-2 text-gray-700">Recipe Title:</label>
        <input id="recipe-title" type="text" v-model="recipeTitle" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
      </div>


      <div class="flex w-full gap-2">
  <div class="flex flex-col w-1/2">
    <label for="prep-time" class="block mb-2 text-gray-700">Preparation Time (mins):</label>
    <input id="prep-time" type="number" v-model="prepTime" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
  </div>
  <div class="flex flex-col w-1/2">
    <label for="cook-time" class="block mb-2 text-gray-700">Cooking Time (mins):</label>
    <input id="cook-time" type="number" v-model="cookTime" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
  </div>
</div>
<div class="flex w-full gap-2">
  <div class="flex flex-col w-1/2">
    <label for="type" class="block mb-2 text-gray-700">Type:</label>
    <select id="type" v-model="type" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
      <option value="breakfast">Breakfast</option>
      <option value="lunch">Lunch</option>
      <option value="dinner">Dinner</option>
    </select>
  </div>
  <div class="flex flex-col w-1/2">
    <label for="cuisine" class="block mb-2 text-gray-700">Cuisine:</label>
    <select id="cuisine" v-model="cuisine" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
      <option value="italian">Italian</option>
      <option value="indian">Indian</option>
      <option value="mexican">Mexican</option>
    </select>
  </div>
</div>



    <div class="w-full">
      <label for="difficulty" class="block mb-2 text-gray-700">Difficulty:</label>
      <select id="difficulty" v-model="difficulty" class="border border-gray-300 rounded-md p-2 mb-4 w-full" required>
        <option value="easy">Easy</option>
        <option value="medium">Medium</option>
        <option value="hard">Hard</option>
      </select>
    </div>
    <div class="w-full">
      <label for="ingredients" class="block mb-2 text-gray-700">Ingredients:</label>
      <div v-for="(ingredient, index) in ingredients" :key="index" class="flex gap-4 items-center mb-4">
        <input v-model="ingredient.name" class="border border-gray-300 rounded-md p-2 w-full" placeholder="Name" required>
        <input v-model.number="ingredient.quantity" type="number" class="border border-gray-300 rounded-md p-2 w-full" placeholder="Quantity" required>
        <button @click.prevent="removeIngredient(index)" v-if="index > 0" class="bg-red-500 text-white py-1 px-3 rounded-md">Remove</button>
      </div>
      <div class="flex flex-row-reverse gap-4">
  <button @click.prevent="addIngredient" class="bg-orange-500 text-white py-1 px-3 rounded-md mt-4">+</button>
      </div>
    </div>
  <button type="submit" class="bg-orange-500 text-white py-2 px-4 rounded-md mx-auto w-auto mb-4">Submit</button>
  </form>
</div>

</template>

<script setup>
import { ref } from "vue";

const recipeTitle = ref('');
const prepTime = ref('');
const cookTime = ref('');
const type = ref('');
const cuisine = ref('');
const difficulty = ref('');
const ingredients = ref([{ name: '', quantity: '' }]);

const submitForm = () => {
  console.log("Recipe Title:", recipeTitle.value);
  console.log("Preparation Time:", prepTime.value);
  console.log("Cooking Time:", cookTime.value);
  console.log("Type:", type.value);
  console.log("Cuisine:", cuisine.value);
  console.log("Difficulty:", difficulty.value);
  console.log("Ingredients:", ingredients.value);
  
  // Clear input fields after submission
  recipeTitle.value = '';
  prepTime.value = '';
  cookTime.value = '';
  type.value = '';
  cuisine.value = '';
  difficulty.value = '';
  ingredients.value = [{ name: '', quantity: '' }];
}

const addIngredient = () => {
  ingredients.value.push({ name: '', quantity: '' });
}

const removeIngredient = (index) => {
  if (ingredients.value.length > 1) {
    ingredients.value.splice(index, 1);
  }
}
</script>

