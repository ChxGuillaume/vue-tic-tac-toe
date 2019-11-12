<template>
  <div id="player">
    <img :src="playerData.img" alt="avatar">
    <h2>{{ playerData.name }}</h2>
    <h3>Score: {{ playerData.score }}</h3>
  </div>
</template>

<script>
export default {
  name: 'Player',
  props: {
    playerData: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>

  #player {
    display: inline-block;
    color: #ffffff;
    margin: 0 250px;

    img {
      border-radius: 100%;
      border: 4px solid white;
    }
  }

</style>
