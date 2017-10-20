<template>
  <main>
    <header>
      <div class="row">
        <div class="col">
          <div class="level">Level: {{ level }}</div>
        </div>
        <div class="col">
          <div class="timer">{{ time }}</div>
        </div>
        <div class="col">
          <button @click="pauseGame" class="btn btn-warning">Pause</button>
        </div>
      </div>
    </header>
    <h1>Game Started!</h1>
    
    <app-game-pause v-if="isPaused" @gameResumed="resumeGame" @gameRestarted="restartGame"></app-game-pause>
    <app-game-result v-if="hasEnded" :level="level" @gameRestarted="restartGame"></app-game-result>
  </main>  
</template>

<script>
import GamePause from '../components/GamePause.vue';
import GameResult from '../components/GameResult.vue';

export default {
  data() {
    return {
      isPaused: false,
      hasEnded: false,
      time: 10,
      level: 1,
      gridNumber: 2,   // start from 2x2
      timerId: ''
    };
  },
  components: {
    appGamePause: GamePause,
    appGameResult: GameResult
  },
  mounted() {
    this.countDown();
  },
  methods: {
    pauseGame() {
      this.isPaused = true;
      this.pauseCountDown();
    },
    resumeGame() {
      this.isPaused = false;
      this.countDown();
    },
    restartGame() {
      this.isPaused = false;
      this.hasEnded = false;
      this.dataReset();
      this.countDown();
    },
    countDown() {
      var vm = this;
      this.timerId = setInterval(function () {
        vm.time -= 1;
      }, 1000);
    },
    pauseCountDown() {
      clearInterval(this.timerId);
    },
    finish() {
      alert(`Time's Up! You passed ${ this.level - 1 } levels!`);
      this.hasEnded = true;
      this.dataReset();
    },
    dataReset() {
      this.isPaused = false;
      this.time = 10;
      this.level = 1,
      this.gridNumber = 2;
      this.timerId = '';
    }
  },
  watch: {
    time(value) {
      if (value <= 0) {
        var vm = this;
        setTimeout(function () {
          vm.pauseCountDown();
          vm.finish();
        }, 300);
      }
    }
  }
}
</script>

<style lang="scss" scoped>
</style>