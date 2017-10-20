<template>
  <main>
    <!-- <div class="container"> -->
      <header class="header">
        <h1>色弱測試</h1>
        <h1>Color Sensitivity Test</h1>
      </header>
      <div class="row">
        <div class="col">
          <button @click="startGame" class="btn btn-primary btn-lg">Start</button>    
        </div>
      </div>
    <!-- </div> -->
  </main>
</template>

<script>
export default {
  name: 'entry',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    startGame() {
      this.$emit('gameStarted');
    }
  }
}
</script>

<style lang="scss" scoped>
main {
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

.header {
  margin-bottom: 40px;
}

</style>
