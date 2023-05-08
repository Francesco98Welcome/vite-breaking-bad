<script>
import axios from 'axios';
import { store } from '../store.js';

export default {
    name: 'AppMain',
    data() {
        return {
            archetypes: [],
            optionsSelect: 'scegli',
            store
        }
    },
    
    // Quando l'oggetto Vue viene creato, imposta il flag di caricamento nello store Vuex a true
    
    created() {
        this.store.loading = true;
        //this.url = "https://db.ygoprodeck.com/api/v7/archetypes.php"
        
        // Effettua una chiamata GET all'API esterna per recuperare gli archetipi
        
        axios
            .get("https://db.ygoprodeck.com/api/v7/archetypes.php")
            .then((response) => {
            
                // Una volta ottenuti i dati dall'API, assegna l'array di archetipi alla proprietà "archetypes"
                // dell'oggetto Vue. Infine, imposta il flag di caricamento nello store Vuex a false
                this.archetypes = response.data
                this.store.loading = false;
            });
    },
    
    // Questa computed property è utilizzata per effettuare una chiamata AJAX ogni volta che l'utente seleziona
    // un archetipo dall'elemento <select> nel template Vue. La funzione setta il flag di caricamento
    // nello store Vuex a true, e fa una chiamata GET all'API esterna passando l'archetipo selezionato come parametro.
    // Una volta ottenuti i dati dall'API, assegna i dati alla proprietà "card" nello store Vuex e imposta
    // il flag di caricamento a false.
    
    computed: {
        onChoise() {
            this.store.loading = true;
            axios
                .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + this.optionsSelect)
                .then((response) => {
                    this.store.card = response.data.data
                    this.store.loading = false;
                });
        },

        /*        props: {
                    cardsList: {
                        type: Array,
                        default: []
                    }
                },*/
    }
}
</script>

<template>
    <main><!--
        <select name="" id="">
            <option selected>Seleziona</option>
            <option value="alien">Alien</option>
            <option value="noble knight">Noble Knight</option>
            <option value="meloudis">Meloudis</option>
        </select>-->
        <select v-model="optionsSelect" @change="onChoise">
            <option selected value="scegli">Seleziona</option>
            <option v-for="archetype in archetypes" :value="archetype.archetype_name">
                {{ archetype.archetype_name }}
            </option>
        </select>
        <div class="containerCard">
            <div class="blackFound">
                Found {{ store.card.length }} cards
            </div>
            <div class="cards">
                <div v-for="card in store.card">
                    <div>
                        <div>
                            <img :src="card.card_images[0].image_url" alt="">
                        </div>
                        <div class="content">
                            <h4>
                                {{ card.name }}
                            </h4>
                            <p>
                                {{ card.archetype }}
                            </p>
                        </div>
                    </div>
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
            padding: 16px;
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

    img {
        width: 100%;
    }

    .content {
        margin-top: -4px;
        height: 100px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        background-color: #d48f38;
    }

    h4 {
        text-transform: uppercase;
        padding-top: 10px;
        color: white;
    }
}
</style>
