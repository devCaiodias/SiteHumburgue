<template>
    <div>
      <Navbar :logo="logo_src" :alt="app_name" />
      <RouterView/>
      <Footer />
    </div>
</template>

<script>
import Footer from './components/Footer.vue';
import Navbar from './components/Navbar.vue';

  export default{
    components: {
    Navbar,
    // eslint-disable-next-line vue/no-reserved-component-names
    Footer
  },
  data() {
    return {
      logo_src: "/img/logo2.png",
      app_name: "logo hanburge",
    }
  }
}
  
</script>

<style>
  * {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  
  div {
    background-color: #29160c;
    
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: 2.5em;
    margin-bottom: 30px;
    color: #ffd21d;
  }
</style>
