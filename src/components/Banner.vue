<template>
   <div id="main-banner">
    <h1> Make Tour Pizza</h1>
   </div>
</template>

<script>

export default{
    name: 'banner'
}
   
</script>

<style scoped>

    #main-banner {
        background-image: url('../img/wallpaperpizza.jpg');
        background-position: 0 250;
        background-size: cover;
        height: 500px;
        display: flex;
        align-items: center;
        justify-content: flex-start;

    }

</style>
