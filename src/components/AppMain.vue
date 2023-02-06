<script>
import cardYuGiOh from './Card.vue';

export default {
    name: 'AppMain',

    props: {
        cardsList: {
            type: Array,
            default: []
        }
    },
    components: {
        cardYuGiOh
    }
}
</script>

<template>
    <main>
        <select name="" id="">
            <option value="bo">Alien</option>
            <option value="bo">e</option>
            <option value="bo">e</option>
        </select>
        <div class="containerCard">
            <div class="blackFound">
                Found 39 cards
            </div>
            <div class="cards">
                <div v-for="card in cardsList">
                    <cardYuGiOh :card="card" />
                </div>
            </div>
        </div>
    </main>
</template>

<style lang="scss">
main {
    background-color: #d48f38;

    select {
        margin: 20px 70px;
        width: 200px;
        border: none;
        padding: 8px;
        border-radius: 10px;
    }

    .containerCard {
        width: 90%;
        margin: 0 auto;
        background-color: white;
        height: 90%;
        padding: 20px;

        .blackFound {
            background-color: black;
            height: 50px;
            color: white;
            padding: 15px;
            width: 98%;
            margin: 0 auto;
        }

        .cards {
            display: flex;
            flex-wrap: wrap;

            >div {
                width: 20%;
                text-align: center;
                padding: 10px;
            }
        }
    }
}
</style>