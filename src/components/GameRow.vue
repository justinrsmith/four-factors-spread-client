<template>
<div class="row border-bottom">
  <div class="col-6 pr-0" :style="{ backgroundColor: teamData.team_color, color: 'white' }">
    <strong>{{ teamData.city }} {{ teamData.nickname }}</strong>
  </div>
  <div class="col-3 border-right">
    {{ teamLine.predicted }}
  </div>
  <div class="col-3 border-right">
    {{ teamLine.actual }}
  </div>
</div>
</template>

<script>
export default {
  props: ['teamData', 'teamLine'],
};
</script>
