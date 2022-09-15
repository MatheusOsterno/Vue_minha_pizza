<template>
    <div class="mensagem-container">
        <p> {{ msg }} </p>
    </div>
</template>

<script>
import { stringifyQuery } from 'vue-router'
    
    export default{
    name: 'Mensagem',
    props: {
        msg: String
    }
    }

</script>

<style scoped>
    .mensagem-container {
        color: #004085;
        background-color: #cce5ff;
        border: 2px solid #bbdaff;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 0 auto;
        margin-bottom: 20px;
    }
    
</style>