<template>
  <Tic_Tac_Game/>
</template>

<script>
import Tic_Tac_Game from './components/Tic_Tac_Game.vue';

export default {
  name: 'App',
  components: {
    Tic_Tac_Game
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
