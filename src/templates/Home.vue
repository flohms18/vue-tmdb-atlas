<script setup>
import { onMounted } from 'vue';


onMounted(() => {
    function james(bond){
        bond = 'Casino Royale';
        console.log(bond)
    }

    james()
})


</script>


<template>
    <div>
        <h1 class="text-3xl font-bold underline">
    Hello world!
  </h1>
    </div>
</template>