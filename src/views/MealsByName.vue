<template>
    <div class="p-8">
        <input 
            type="text" 
            v-model="keyword"
            class="rounded border-2 border-gray-200 w-full" 
            placeholder="Search for Meals"
            @change="searchMeals"
            />
    </div>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-3 p-8">
        <div v-for="meal of meals" :key="meal.idMeal" class="bg-white shadow rounded-xl">
            <img :src="meal.strMealThumb" :alt="strMeal" class="rounded-t-xl w-full h-48 object-cover">
            <div class="p-3">
                <h3 class="font-semibold">{{ meal.strMeal }}</h3>
                <p class="mb-4">Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam tenetur quod autem ex fugiat dicta nulla quidem quis commodi.</p>
                <div class="flex items-center justify-between">
                    <a :href="meal.strYoutube" target="_blank" class="px-3 py-2 rounded border-2 text-white border-red-600 bg-red-500 hover:red-600 transition-colors">Youtube</a>
                    <router-link to="/" class="px-3 py-2 rounded border-2 text-white border-purple-600 bg-purple-500 hover:purple-600 transition-colors">
                        View  
                    </router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed } from '@vue/reactivity'
import { ref } from 'vue';
import axiosClient from '../axiosClient';
import store from '../store';

const keyword = ref('');
const meals = computed(() => store.state.searchedMeals);

function searchMeals(){
    store.dispatch('searchMeals', keyword.value)
}

</script>