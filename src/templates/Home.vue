<script setup>
import axios from 'axios';
import { ref } from 'vue'

const item = ref([])
const trailerKey = ref(null)
const showTrailerModal = ref(false)

function callAPI() {
        const api_key = import.meta.env.VITE_TMDB_API_KEY
        const options_search = {
            method : 'GET',
            url: 'https://api.themoviedb.org/3/search/movie?query=' + searchMovie.value + '&include_adult=false&language=en-US&page=1',
            headers : {
                accept : 'application/json', Authorization : 'Bearer ' + api_key
            }
        };
        axios
            .request(options_search)
            .then(res => item.value = res.data.results)
            .then(res => console.log(res))
            .catch(err => console.error(err));
    }

function watchTrailer(movieId) {
    const api_key = import.meta.env.VITE_TMDB_API_KEY
    const options_trailer = {
        method : 'GET',
        url: `https://api.themoviedb.org/3/movie/${movieId}/videos`,
        headers : {
            accept : 'application/json', Authorization : 'Bearer ' + api_key
        }
    };
    axios
        .request(options_trailer)
        .then(res => {
            const videos = res.data.results
            const video = videos.find(v => v.type === 'Trailer' && v.site === 'YouTube')
                || videos.find(v => v.site === 'YouTube')
            if (video) {
                trailerKey.value = video.key
                showTrailerModal.value = true
            } else {
                console.error('No trailer available for this movie')
            }
        })
        .catch(err => console.error(err));
}

function closeTrailer() {
    showTrailerModal.value = false
    trailerKey.value = null
}

const searchMovie = defineModel()






</script>


<template>
    <div class="flex flex-col items-center py-5 w-screen bg-dark-brand items-center min-h-screen">
        <h1 class="text-blue-brand font-display text-center text-4xl py-20">TMDB App</h1>
           <p class="text-white-brand text-center font-display pt-5 text-xl">Enter the movie's name</p> 
           <input class="max-w-2xs placeholder:text-gray-500 w-3xs pl-3 text-white-brand outline-gray-600 mt-5 rounded-md" v-model="searchMovie" placeholder="Dune">
            <button type="button" @click="callAPI()" class="text-blue-brand font-display mt-5 px-6 py-2 flex items-center justify-center rounded-md border border-blue-brand">Search</button>
            
            
            <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-4 p-4 text-center">
                <div v-for="movie in item" :key="movie.id" class="flex flex-col">
                    <img
                        v-if="movie.poster_path"
                        :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
                        :alt="movie.title"
                        class="w-full aspect-2/3 object-cover rounded-lg"
                    >
                    <div v-else class="w-full aspect-2/3 rounded-lg bg-dark-brand/10 flex items-center justify-center text-sm text-white-brand">
                        No poster
                    </div>
                    <p class="mt-2 text-base font-display truncate text-blue-brand font-display">{{ movie.title }}</p>
                    <p class="text-sm text-white-brand font-display">{{ movie.release_date }}</p>
                    <button class="text-white-brand" @click="watchTrailer(movie.id)">Watch the trailer</button>
                </div>
            </div>

            <div
                v-if="showTrailerModal"
                class="fixed inset-0 z-50 flex items-center justify-center bg-black/70"
                @click.self="closeTrailer()"
            >
                <div class="bg-dark-brand border border-blue-brand rounded-md p-4 w-11/12 max-w-3xl">
                    <div class="flex justify-end mb-2">
                        <button class="text-blue-brand font-display" @click="closeTrailer()">Close</button>
                    </div>
                    <div class="relative w-full aspect-video">
                        <iframe
                            class="absolute inset-0 w-full h-full rounded-md"
                            :src="`https://www.youtube.com/embed/${trailerKey}`"
                            allow="autoplay; encrypted-media"
                            allowfullscreen
                        ></iframe>
                    </div>
                </div>
            </div>
    </div>

    

    
</template>