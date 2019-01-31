<template>
  <div id="app">
    <player-cmp></player-cmp>
  </div>
</template>

<script>
import PlayerCmp from './components/PlayerCmp'

export default {
  name: 'app',
  components: {
    PlayerCmp
  }
}
</script>


<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
