<template>
<div>
  <app-header>
    <div class="alert alert-secondary">
      Model lines are produced primarly using
      <a href="https://www.basketball-reference.com/about/factors.html">
        Four Factors
      </a> data which is then weighted accordingly and used in the projections.
    </div>
  </app-header>
  <games :games="games"></games>
  <app-footer>
    <div class="alert alert-info">
      <p>
        <strong>*</strong> Model is updated daily at 5:30 am EST
      </p>
      <p>
        <strong>**</strong> Actual line data is based on Caesars Sportsbook and is updated daily at
        7:15 am EST and 11:15 am EST
      </p>
    </div>
  </app-footer>
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
      .get('https://4vkfarr292.execute-api.us-east-1.amazonaws.com/dev')
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
