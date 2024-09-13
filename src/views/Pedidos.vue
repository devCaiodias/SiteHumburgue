<template>
  <div class="main-container">
    <h1>Gerenciar Pedidos !</h1>

    <Dashboard />
  </div>
</template>

<script>
import Dashboard from '@/components/Dashboard.vue';

  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name: "Pedidos",
    components: {
      Dashboard
    }

  }
</script>

<style scoped>
  
</style>