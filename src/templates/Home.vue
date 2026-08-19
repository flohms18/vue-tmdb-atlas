<script setup>
import axios from 'axios';
import { ref } from 'vue'

const item = ref([])


function callAPI() {
        const api_key = import.meta.env.VITE_TMDB_API_KEY
        const options = {
            method : 'GET',
            url: 'https://api.themoviedb.org/3/search/movie?query=' + searchMovie.value + '&include_adult=false&language=en-US&page=1',
            headers : {
                accept : 'application/json', Authorization : 'Bearer ' + api_key
            }
        };
        axios
            .request(options)
            .then(res => item.value = res.data.results)
            .then(res => console.log(res))
            .catch(err => console.error(err));
        
    }

const searchMovie = defineModel()






</script>


<template>
    <div class="flex flex-col items-center py-5 w-screen bg-dark-brand items-center h-screen">
        <h1 class="text-blue-brand font-display text-center text-4xl py-20">TMDB App</h1>
           <p class="text-white-brand text-center font-display pt-5">Enter the movie's name</p> 
           <input class="max-w-2xs placeholder:text-gray-500 w-3xs pl-3 text-white-brand outline-gray-600 mt-5 rounded-md" v-model="searchMovie" placeholder="Dune">
            <button type="button" @click="callAPI()" class="text-blue-brand font-display pt-5">Search</button>
            
            
            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 p-4 text-left">
                <div v-for="movie in item" :key="movie.id" class="flex flex-col">
                    <img
                        v-if="movie.poster_path"
                        :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
                        :alt="movie.title"
                        class="w-full aspect-2/3 object-cover rounded-lg"
                    >
                    <div v-else class="w-full aspect-2/3 rounded-lg bg-dark-brand/10 flex items-center justify-center text-sm">
                        No poster
                    </div>
                    <p class="mt-2 text-base font-display truncate">{{ movie.title }}</p>
                    <p class="text-sm text-dark-brand/70">{{ movie.release_date }}</p>
                    <button @click="">Watch the trailer</button>
                </div>
            </div>
    </div>

    

    
</template>