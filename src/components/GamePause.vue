<template>
  <div class="lightbox">
    <div class="container">
      <header class="header">
        <h1>Pause</h1>  
      </header>
      <div class="row">
        <div class="col">
          <button @click="resumeGame" class="btn btn-success btn-lg">Continue!</button>
          <button @click="restartGame" class="btn btn-danger btn-lg">restart</button>
        </div>
      </div>  
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    resumeGame() {
      this.$emit('gameResumed');
    },
    restartGame() {
      this.$emit('gameRestarted');
    }
  }
}
</script>

<style lang="scss" scoped>
.lightbox {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  background-color: #efefef;
  z-index: 100;
}
</style>