<template>
    <Navbar />
    <router-view />
    <Rodape /> 
  
</template>

<script>
import Navbar from './components/Navbar.vue'
import Rodape from './components/Rodape.vue'
export default {
  components: {
    Navbar,
    Rodape
  },
  
}
</script>

<style>
  *{
    font-family: Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
