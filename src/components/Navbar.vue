<template>
    <div id="nav">
        <router-link to="/" id="logo-url"> <img src="../img/logo.png" alt="app_name" id="logo"></router-link>
        <router-link to="/" id="home"> Home </router-link>
        <router-link to="/pedidos" id="Pedidos"> Pedidos </router-link>
    </div>
</template>

<script>
    export default{
        name: "Navbar",

    Data() {
        return {
        logo_src: './img/logo.png',
        app_name: "Make Your Pizza"
     }
    }
}
</script>

<style scoped>
    #nav { 
        background: #222;
        border-bottom: 4px solid #111;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
        font-size: 25px;
    }
    
    #nav #logo-url{
        margin: auto;
        margin-left: 0;
        height: 50%;
        width: 50%;
        object-fit: contain;

    }
    #nav #logo-url #logo {
        max-width: 60px;
    }

    #nav a {
        color: #FCBA03;
        text-decoration: none;
        margin: 12px;
        transition: 0.6s;
    }
    
    #nav a:hover{
        color: #FFF ;
    }

</style>