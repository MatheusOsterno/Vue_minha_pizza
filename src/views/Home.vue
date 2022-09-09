<template>
  <banner />
  <div class="main-container">
    <h1> Monte sua pizza: </h1>
    <pizzaform />
  </div>
</template>

<script>
import banner from '../components/Banner.vue'
import pizzaform from '../components/Pizzaform.vue'

export default {
  name: "Home",
  components: {
    banner,
    pizzaform
  }
}

</script>

<style scoped>

</style>