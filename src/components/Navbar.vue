<template>
    <div id="nav">
        <RouterLink to="/" id="logo_url">
            <img :src="logo" :alt="alt" id="logo">
        </RouterLink>
        <RouterLink to="/">Home</RouterLink> 
        <RouterLink to="/Pedidos">Pedidos</RouterLink>
    </div>
</template>

<script>
    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Navbar',
        props: ["logo", "alt", "tamanho"]
    }
</script>

<style scoped>
    #nav {
        background-color: black;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    #nav #logo_url{
        margin: auto;
        margin-left: 0;
    }

    #logo {
        width: 112px;
    }

    #nav a {
        color: #ffd21d;
        text-decoration: none;
        margin: 12px;
        transition: .5;
        font-size: 1.3em;
    }
    
    #nav a:hover {
        opacity: .8;
    }
</style>