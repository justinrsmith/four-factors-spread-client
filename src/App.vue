<template>
<div id="app" class="container">
  <div v-for="game in games" class="row">
    <div class="col border-bottom">
      <div class="row">
        <div class="col-3" :style="{ backgroundColor: game.home.team_color, color: 'white' }">
          {{ game.home.city }} {{ game.home.nickname }}
        </div>
        <div class="col-3">
          {{ game.line.home.predicted }}
        </div>
        <div class="col-3">
          {{ game.line.home.actual }}
        </div>
      </div>
      <div class="row">
        <div class="col-3" :style="{ backgroundColor: game.visitor.team_color, color: 'white' }">
          {{ game.visitor.city }} {{ game.visitor.nickname }}
        </div>
        <div class="col-3">
          {{ game.line.visitor.predicted }}
        </div>
        <div class="col-3">
          {{ game.line.visitor.actual }}
        </div>
      </div>
    </div>
  </div>
</div>

</template>

<script>
import axios from 'axios';
import { getMainColor } from 'nba-color';

export default {
  name: 'app',
  data: function() {
    return {
      games: [],
    };
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
        });
      });
  },
};
</script>

<style>
</style>
