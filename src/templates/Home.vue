<script setup>
import { onMounted } from 'vue';
import axios from 'axios';




onMounted(() => {
    function james(bond){
        bond = 'Casino Royale';
        console.log(import.meta.env.VITE_TMDB_API_KEY)
    }

    james()

    function callAPI(api_key) {
        api_key = import.meta.env.VITE_TMDB_API_KEY
        const options = {
            method : 'GET',
            url : 'https://api.themoviedb.org/3/movie/popular',
            headers : {
                accept : 'application/json', Authorization : 'Bearer ' + api_key
            }
        };
        axios
            .request(options)
            .then(res => console.log(res.data))
            .catch(err => console.error(err));
    }

    callAPI()
})


</script>


<template>
    <div class="flex flex-col h-screen bg-dark-brand w-screen text-center py-5 text-4xl">
        <h1 class="text-blue-brand font-display">TMDB App</h1>
        
    </div>
</template>