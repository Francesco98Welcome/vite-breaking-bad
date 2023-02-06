<script>
export default {
    name: 'AppHeader',
    data() {
        return {

        }
    },
    props: {
        msg: String,
    }
}
</script>

<template>
    <header>
        <img src="../assets/logo.png" alt="">
        <h1>Yu-Gi-Oh Api</h1>
    </header>
</template>

<style lang="scss">
header {
    padding: 10px;
    background-color: white;
    font-size: 20px;
    display: flex;
    align-items: center;

    img {
        width: 60px;
    }

    h1 {
        font-size: 22px;
        margin-left: 10px;
    }
}
</style>