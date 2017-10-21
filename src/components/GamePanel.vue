<template>
  <div>
    <div class="panel" ref="panel">
      <!-- grid -->
    </div>
    <button @click="nextLevel" class="btn btn-success">Next Level</button>
  </div>
</template>

<script>
  export default {
    props: [ 'gridSize' ],
    mounted() {
      this.setPanel(this.gridSize, this.totalBricks);
    },
    computed: {
      totalBricks() {
        return this.gridSize * this.gridSize;
      }
    },
    methods: {
      nextLevel() {
        this.$emit('levelup');
      },
      setPanel(size, totalBricks) {
        this.setGridSize(size);
        this.setGridItems(totalBricks);
      },
      setGridSize(size) {
        document.documentElement.style.setProperty("--grid-size", size);
      },
      setGridItems(totalBricks) {
        var panel = this.$refs.panel;
        // remove old elements
        while (panel.firstChild) {
          panel.removeChild(panel.firstChild);
        }
        if (totalBricks === 0) {
          return;
        }
        // add new elements
        for (var i = 0; i < totalBricks; i++) {
          let brick = document.createElement('div');
          brick.classList.add('brick');
          panel.append(brick);
        }
      }
    },
    watch: {
      gridSize(val) {
        this.setPanel(val, this.totalBricks);
      }
    }
  }
</script>

<style lang="scss">
  :root {
    --grid-size: 2;
  }
  .panel {
    width: 400px;
    height: 400px;
    display: grid;
    grid-template-rows: repeat(var(--grid-size), 1fr);
    grid-template-columns: repeat(var(--grid-size), 1fr);
    grid-gap: 10px;
    border: 10px solid #FFBB00;
    border-radius: 10px;
    background-color: #FFBB00;
  }
  .brick {
    border-radius: 5px;
    background-color: #FFF76B;
  }
</style>