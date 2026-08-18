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
            .catch(err => console.error(err));
    }

const searchMovie = defineModel()



</script>


<template>
    <div class="flex flex-col w-screen text-center py-5 text-4xl">
        <h1 class="text-blue-brand font-display">TMDB App</h1>
           <span>My input</span> <input v-model="searchMovie">
            <button type="button" @click="callAPI()">Click Me!</button>
            <ul>
                <li v-for="movie in item" :key="movie.id">
                    {{ movie.title }} ({{ movie.release_date?.slice(0, 4) }})
                </li>
            </ul>

    </div>
</template>