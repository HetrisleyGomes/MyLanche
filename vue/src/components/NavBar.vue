<template>
    <div id="nav">
        <div id="logo_url">
            <router-link to="/" >
            <img src="/img/logo.png" alt="logo" id="logo">
            </router-link>
            <span id="titulo">My-Lanche</span>
        </div>

        <router-link to="/">Home</router-link>
        <router-link to="/pedidos">Pedidos</router-link>
        <router-link to="/lojas" v-show="isClient">Lojas</router-link>
        <router-link to="/about">About</router-link>
    </div>
</template>

<script>
export default {
    name: 'NavBar',
    props: {isClient:Boolean}
}
</script>

<style scoped>
    #nav{background-color: #261bc0; border-bottom: 4px solid #2b0070;
    padding: 30px 50px; display: flex; justify-content: flex-end; align-items: flex-end;}
    #nav #logo_url{margin: 0 auto; margin-top: -10px; margin-left: 0px; display: flex;flex-direction: column; align-items: center;}
    #logo{width: 40px; height: 40px;}
    #nav #titulo{font-weight: bold; color: #fff}
    #nav a {color: #fcba03; text-decoration: none; margin: 10px;
    transition: .3s;}
    #nav a:hover{color: #fff;}
</style>