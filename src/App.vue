<template>
  <div class="container">
    <app-entry v-if="!isGameStarted" @gameStarted="gameStarted"></app-entry>
    <app-game v-else></app-game>
  </div>
</template>

<script>
import Entry from './pages/Entry.vue';
import Game from './pages/Game.vue';

export default {
  // name: 'app',
  data () {
    return {
      isGameStarted: false
    }
  },
  components: {
    appEntry: Entry,
    appGame: Game
  },
  methods: {
    gameStarted() {
      this.isGameStarted = true;
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Montserrat', "source-han-sans-traditional", sans-serif;
  font-style: normal;
  font-weight: 400; // han-sans-trad
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.btn {
  cursor: pointer;
}

.header {
  margin-bottom: 40px;
}

</style>
