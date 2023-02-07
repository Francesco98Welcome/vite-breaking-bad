<script>
import axios from 'axios';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    AppMain
  },

  data() {
    return {
      cards: []
    }
  },

  mounted() {
    axios
      .get('https://db.ygoprodeck.com/api/v7/cardinfo.php')
      .then((response) => {

        this.cards = response.data.data.slice(0, 10);
        console.log(response)
        console.log(response.data.data.slice(0, 10));
        //console.log(this.cards)
      })
  }
}
</script>

<template>
  <AppHeader />

  <AppMain :cardsList="cards" />
</template>

<style lang="scss">
@import './styles/main.scss';
</style>
