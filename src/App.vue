<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
import { store } from './store.js';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain
  },

  data() {
    return {
      cards: [],
      choose: 'Alien',
      url: '',
      store
    }
  },

  created() {
    /*
    axios
      .get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
      .then((response) => {

        this.cards = response.data.data.slice(0, 10);
        console.log(response)
        console.log(response.data.data.slice(0, 10));
        //console.log(this.cards)
      })
      */
    this.url = "https://db.ygoprodeck.com/api/v7/cardinfo.php";
    this.store.loading = true;
    axios
      .get(this.url)
      .then((response) => {
        this.store.card = response.data.data.slice(0, 20);
        this.store.loading = false;
      });
  }
}
</script>

<template>
  <AppHeader />

  <AppMain />
</template>

<style lang="scss">
@import './styles/main.scss';
</style>
