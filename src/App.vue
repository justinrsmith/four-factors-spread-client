<template>
<div id="app">
  <nav class="navbar navbar-dark mb-3" style="background-color: #17408B;">
    <span class="navbar-brand mb-0 h1">Four Factors Model</span>
  </nav>
  <div class="container">
    <div class="col-lg-6 offset-lg-3 col-md-12 p-0">
      <div class="row">
        <div class="col-6"><strong>Team</strong></div>
        <div class="col-3"><strong>Model</strong></div>
        <div class="col-3"><strong>Actual</strong></div>
      </div>
      <div v-for="game in games" class="row mb-4" :key="game.id">
        <div class="col border-top border-bottom">
          <div class="row">
            <div class="col-6 pr-0" :style="{ backgroundColor: game.visitor.team_color, color: 'white' }">
              <strong>{{ game.visitor.city }} {{ game.visitor.nickname }}</strong>
            </div>
            <div class="col-3 border-right">
              {{ game.line.visitor.predicted }}
            </div>
            <div class="col-3 border-right">
              {{ game.line.visitor.actual }}
            </div>
          </div>
          <div class="row border-top border-bottom">
            <div class="col-6 pr-0" :style="{ backgroundColor: game.home.team_color, color: 'white' }">
              <strong>{{ game.home.city }} {{ game.home.nickname }}</strong>
            </div>
            <div class="col-3 border-right">
              {{ game.line.home.predicted }}
            </div>
            <div class="col-3 border-right">
              {{ game.line.home.actual }}
            </div>
          </div>
          <div class="row bg-light border-right border-left">
            <div class="col-6">
              <strong>Game Information</strong>
            </div>
          </div>
          <div class="row bg-light border-right border-left">
            <div class="col">
              <div class="row">
                <div class="col">
                  Location: {{ game.home.city }}
                </div>
              </div>
              <div class="row">
                <div class="col">
                  Date: {{ date }}
                </div>
              </div>
              <div class="row">
                <div class="col">
                  Time: {{ game.time }} EST
                </div>
              </div>
            </div>
            <div class="col">
              <div class="row">
                <div class="col">
                  Visitor Record: {{ game.visitor.record }}
                </div>
              </div>
              <div class="row">
                <div class="col">
                  Home Record: {{ game.home.record }}
                </div>
              </div>
              <div class="row">
                <div class="col">
                  <a target="_blank" :href="'https://stats.nba.com/game/' + game.id">View Game Detail</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import axios from 'axios';
import { getMainColor } from 'nba-color';
import moment from 'moment';

export default {
  name: 'app',
  data: function() {
    return {
      games: [],
      date: moment().format('MM/DD/YY'),
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
          game.time = moment(game.time, 'hh:mm').format('hh:mm A');
        });
      });
  },
};
</script>

<style>
</style>
