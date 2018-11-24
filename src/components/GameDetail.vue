<template>
  <div>
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
            Date: {{ game.date }}
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
            {{ game.visitor.abbreviation }} Record: {{ game.visitor.record }}
          </div>
        </div>
        <div class="row">
          <div class="col">
            {{ game.home.abbreviation }} Record: {{ game.home.record }}
          </div>
        </div>
        <div class="row">
          <div class="col">
            <a target="_blank" :href="'https://stats.nba.com/game/' + game.id">View Game Detail</a>
          </div>
        </div>
      </div>
    </div>
    <div v-if="game.home.b2b || game.visitor.b2b" class="row bg-light border-right border-left">
      <div class="col">
        <div class="row">
          <div class="col">
            On B2B: {{ !game.home.b2b ? '' : game.home.abbreviation }} {{ !game.visitor.b2b ? '' : game.visitor.abbreviation }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['game'],
};
</script>
