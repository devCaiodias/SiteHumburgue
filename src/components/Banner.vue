<template>
    <div id="main-banner">
    </div>
</template>

<script>
    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: "Banner"
    }
</script>

<style scoped>
    #main-banner{
        background-image: url('/img/banner.png');
        background-position: center bottom;
        background-size: cover;
        background-repeat: no-repeat;
        height: 450px;
    }
</style>