<template>
  <div id="app">
    <TicTacToe></TicTacToe>
  </div>
</template>

<script>
import TicTacToe from './components/TicTacToe.vue';

export default {
  name: 'app',
  components: { TicTacToe },
};
</script>

<style lang="scss">
  html, body {
    background: #424242;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
