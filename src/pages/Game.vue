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
    <app-game-panel :gridSize="gridSize" @levelup="gotoNextLevel"></app-game-panel>
    
    <app-game-pause v-if="isPaused" @gameResumed="resumeGame" @gameRestarted="restartGame"></app-game-pause>
    <app-game-result v-if="hasEnded" :level="level" @gameRestarted="restartGame"></app-game-result>
  </main>  
</template>

<script>
import GamePause from '../components/GamePause.vue';
import GameResult from '../components/GameResult.vue';
import GamePanel from '../components/GamePanel.vue';
const gameDefaultValues = {
  isPaused: false,
  hasEnded: false,
  time: 60,
  level: 1,
  gridSize: 2,   // start from 2x2
  timerId: ''
}

export default {
  data() {
    return {
      isPaused: gameDefaultValues.isPaused,
      hasEnded: gameDefaultValues.hasEnded,
      time: gameDefaultValues.time,
      level: gameDefaultValues.level,
      gridSize: gameDefaultValues.gridSize,
      timerId: gameDefaultValues.timerId
    };
  },
  components: {
    appGamePause: GamePause,
    appGameResult: GameResult,
    appGamePanel: GamePanel
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
    gotoNextLevel() {
      this.level += 1;
      this.gridSize += 1;
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
    },
    dataReset() {
      this.isPaused = gameDefaultValues.isPaused;
      this.time = gameDefaultValues.time;
      this.level = gameDefaultValues.level;
      this.gridSize = gameDefaultValues.gridSize;
      this.timerId = gameDefaultValues.timerId;
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