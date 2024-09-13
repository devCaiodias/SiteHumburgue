<template>
    <footer id="footer">
        <p>BURGERS &copy; 2024</p>
    </footer>
</template>

<script>
    export default {
        // eslint-disable-next-line vue/multi-word-component-names, vue/no-reserved-component-names
        name: 'Footer'
    }
</script>

<style scoped>
    #footer {
        height: 182px;
        background-color: rgb(0, 0, 0);
        border-top: 4px solid #000000;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        margin: 50px 0px 0px 0px;
    }

    #footer p {
        color: #ffd21d;
    }
</style>