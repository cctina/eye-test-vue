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
    props: [ 'level', 'gridSize' ],
    data() {
      return {
        targetCol: 0,
        targetRow: 0
      };
    },
    mounted() {
      this.setPanel(this.gridSize, this.totalBricks);
      this.setTargetItem(this.gridSize);
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
          if (i === 0) {
            brick.classList.add('brick-target');
          }
          panel.append(brick);
        }
      },
      setTargetItem(size) {
        this.targetCol = Math.round(Math.random() * (size - 1)) + 1;
        this.targetRow = Math.round(Math.random() * (size - 1)) + 1;
        document.documentElement.style.setProperty("--grid-start-column", this.targetCol);
        document.documentElement.style.setProperty("--grid-start-row", this.targetRow);
      }
    },
    watch: {
      level() {
        this.setPanel(this.gridSize, this.totalBricks);
        this.setTargetItem(this.gridSize);
      }
    }
  }
</script>

<style lang="scss">
  :root {
    --grid-size: 2;
    --grid-start-column: 1;
    --grid-start-row: 1;
    --panel-color: #FFBB00;
    --brick-color: #FFF76B;
    --tartget-brick-color: #FFF31F;
  }
  .panel {
    width: 400px;
    height: 400px;
    display: grid;
    grid-template-rows: repeat(var(--grid-size), 1fr);
    grid-template-columns: repeat(var(--grid-size), 1fr);
    grid-gap: 10px;
    border: 10px solid var(--panel-color);
    border-radius: 10px;
    background-color: var(--panel-color);
  }
  .brick {
    border-radius: 5px;
    background-color: var(--brick-color);
  }
  .brick-target {
    @extend .brick;
    grid-column: var(--grid-start-column) / span 1;   // x-axis value
    grid-row: var(--grid-start-row) / span 1;         // y-axis value
    background-color: #FFF;
    background-color: var(--tartget-brick-color);
  }
</style>