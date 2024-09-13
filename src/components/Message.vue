<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<script>
    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: 'Message',
        props: {
            msg: String
        }
    }
</script>

<style scoped>
    .message-container {
        color: #ffd21d;
        background-color: #A66124;
        border: 2px solid black;
        border-radius: 10px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
        
    }

    p {
        text-align: center;
        font-weight: bold;
    }
</style>