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
    <div>
        <h1 class="text-3xl font-bold bg-dark-brand underline">
    Hello world!
  </h1>
    </div>
</template>