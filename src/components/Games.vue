<template>
  <div class="col-lg-6 offset-lg-3 col-md-12 p-0">
    <div class="row">
      <div class="col-6"><strong></strong></div>
      <div class="col-3"><strong>Model</strong></div>
      <div class="col-3"><strong>Actual*</strong></div>
    </div>
    <div v-for="game in games" class="row mb-4" :key="game.id">
      <div class="col border-top border-bottom">
        <game-row :team-data="game.visitor" :team-line="game.line.visitor"></game-row>
        <game-row :team-data="game.home" :team-line="game.line.home"></game-row>
        <game-detail :game="game"></game-detail>
      </div>
    </div>
  </div>
</template>

<script>
import GameRow from './GameRow.vue';
import GameDetail from './GameDetail.vue';

export default {
  props: ['games'],
  components: {
    // eslint-disable-next-line
    gameRow: GameRow,
    // eslint-disable-next-line
    gameDetail: GameDetail,
  },
};
</script>
