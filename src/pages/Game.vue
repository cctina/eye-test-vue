<template>
  <main>
    <h1>Game Started!</h1>  
    <button @click="pauseGame" class="btn btn-warning btn-lg">Pause</button>
    
    <app-game-pause v-if="isPaused" @gameResumed="resumeGame" @gameRestarted="restartGame"></app-game-pause>
  </main>  
</template>

<script>
import GamePause from '../components/GamePause.vue';

export default {
  data() {
    return {
      isPaused: false
    };
  },
  components: {
    appGamePause: GamePause
  },
  methods: {
    pauseGame() {
      this.isPaused = true;
    },
    resumeGame() {
      this.isPaused = false;
    },
    restartGame() {
      this.isPaused = false;
      // clean data
    }
  }
}
</script>

<style lang="scss" scoped>
</style>