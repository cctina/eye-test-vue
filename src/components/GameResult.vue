<template>
  <div class="page">
    <div class="container">
      <header class="header">
        <h1>Result</h1>
        <p>You are a level-{{ level - 1 }} color master!</p>
      </header>
      <div class="row">
        <div class="col">
          <button @click="restartGame" class="btn btn-danger btn-lg">Play Again</button>
        </div>
      </div>  
    </div>
  </div>  
</template>

<script>
  export default {
    props: [ 'level' ],
    methods: {
      restartGame() {
        this.$emit('gameRestarted');
      }
    }
  }
</script>

<style lang="scss" scoped>
.page {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  background-color: #efefef;
  z-index: 100;
}
</style>