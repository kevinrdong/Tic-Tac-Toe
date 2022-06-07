<template>
    <div id="app">
    <div class="status">it's your turn: {{showStep(player6)}}</div>
    <button v-on:click="reset">Reset</button>
      <div class="square" :key="id">
        <div v-for="(grid,id) in grids" class="squares"  v-on:click="move(id)" :key="id" >{{showStep(grid)}}</div>
      </div>
  </div>
</template>
  

<script>
export default {
    name: "App",
    data() {
      return {
        test: 'asd',
        moveMent: '',
        player: 1,
        grids: [
          0, 0, 0,
          0, 0, 0,
          0, 0, 0
        ],
        winner: 0,
      };
    },
    methods: {

      move(id) {
        if (this.grids[id] !== 0) return;
        else if (this.winner !== 0) return;
        else this.$set(this.grids, id, this.player);
        this.player = -this.player;
        
      },
      showStep (val) {
      return val === 0 ? '' : val === 1 ? 'O' : 'X';
    },
      reset() {
        this.moveMent = ''
        this.status = "O"
        this.player = 1
        this.grids = [0, 0, 0, 0, 0, 0, 0, 0, 0];
      },
    }
   
  };
</script>

<style lang="scss">
.square {
  display: flex;
  flex-wrap: wrap;
  width: 400px;
  height: 400px;
  align-content: flex-start;
  .squares {
    font-size: 60px;
    width: 33%;
    height: 33%;
    border: 1px solid black;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    }
  
  } 


</style>
