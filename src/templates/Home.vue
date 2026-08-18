<script setup>
import { onMounted } from 'vue';
import axios from 'axios';




onMounted(() => {
    function james(bond){
        bond = 'Casino Royale';
        console.log(import.meta.env.DB_PASSWORD)
    }

    james()

    function callAPI() {
        axios.get('https://jsonplaceholder.typicode.com/users')
            .then(res => console.log(res.data))
    }

    callAPI()
})


</script>


<template>
    <div class="flex flex-col h-screen bg-dark-brand w-screen text-center py-5 text-4xl">
        <h1 class="text-blue-brand font-display">TMDB App</h1>
        
    </div>
</template>