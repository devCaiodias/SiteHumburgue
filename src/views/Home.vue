<template>
  <div class="main-container">
  <Banner />
    <h1>Monte o seu Burge! </h1>
    <BurgerForm />
  </div>
</template>

<script>
import BurgerForm from '@/components/BurgerForm.vue';
import Banner from '../components/Banner.vue';

  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Home",
    components: {
      // eslint-disable-next-line vue/no-unused-components
      Banner,
      BurgerForm
    }
  }
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
  }

  h1 {
    margin: 30px 0px;
  }
</style>