<template>
   <div id="main-banner">
    <h1> Make Your Pizza</h1>
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
        background-position: 200 -250;
        background-size: cover;
        height: 600px;
        display: flex;
        align-items: center;
        justify-content: flex-end;
    }

    #main-banner h1 {
        color: #fff;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
    }
</style>
