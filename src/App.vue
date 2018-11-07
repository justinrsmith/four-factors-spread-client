<template>
<div>
  <app-header></app-header>
  <games :games="games"></games>
  <app-footer>* Caesars Sportsbook</app-footer>
</div>
</template>

<script>
import axios from 'axios';
import { getMainColor } from 'nba-color';
import moment from 'moment';
import Header from './components/Header.vue';
import Games from './components/Games.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'app',
  data: function() {
    return {
      games: [],
    };
  },
  components: {
    // eslint-disable-next-line
    appHeader: Header,
    Games: Games,
    // eslint-disable-next-line
    appFooter: Footer,
  },
  created: function() {
    let vm = this;
    axios
      .get('https://25idbhr17d.execute-api.us-east-1.amazonaws.com/dev')
      .then((response) => {
        vm.games = response.data;
        vm.games.forEach((game) => {
          game.home.team_color = getMainColor(game.home.team_key).hex;
          game.visitor.team_color = getMainColor(game.visitor.team_key).hex;
          game.time = moment(game.time, 'hh:mm').format('hh:mm A');
          game.date = moment(game.date).format('MM/DD/YY');
        });
      });
  },
};
</script>

<style>
</style>
