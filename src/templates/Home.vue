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
            url: 'https://api.themoviedb.org/3/search/movie?query=inception&include_adult=false&language=en-US&page=1',
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

const model = defineModel()



</script>


<template>
    <div class="flex flex-col w-screen text-center py-5 text-4xl">
        <h1 class="text-blue-brand font-display">TMDB App</h1>  
           <span>My input</span> <input v-model="model">
           {{ model }}


    </div>
</template>