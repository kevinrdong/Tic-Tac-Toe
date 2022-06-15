<template>
  <div id="app">
    <div class="status">it's your turn: {{ showStep(player) }}</div>
    <div class="tell" v-if="winner!==0">The winner is {{showStep(winner)}}</div>
    <button v-on:click="reset">Reset</button>
    <div class="square" :key="id">
      <div
        v-for="(grid, id) in grids"
        class="squares"
        v-on:click="move(id)"
        :key="id"
      >
        {{ showStep(grid) }}
      </div>
    </div>
  </div>
</template>
  

<script>
export default {
  name: "App",
  data() {
    return {
      moveMent: "",
      player: 1,
      grids: [0, 0, 0, 0, 0, 0, 0, 0, 0],
      winner: 0,
      winLines: [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ],
    };
  },
  methods: {
    move(id) {
      if (this.grids[id] !== 0) return;
      else if (this.winner !== 0) return;
      else this.$set(this.grids, id, this.player);
      this.player = -this.player;
      this.getWinner();
    },
    showStep(val) {
      if (val ===0 )
      return "";
      else if (val === 1)
      return "O";
      else if (val === -1)
      return "X";
      else if (val === 3)
      return "tie!";
      // return val === 0 ? "" : val === 1 ? "O" : "X";
      
    },
    reset() {
      this.moveMent = "";
      this.status = "O";
      this.player = 1;
      this.grids = [0, 0, 0, 0, 0, 0, 0, 0, 0];
      this.winner = 0;
    },
    getWinner() {
      for (let i = 0; i < 8; i++) {
        let winLine = this.winLines[i];
        let [a,b,c] = winLine;
        let sum = this.grids[a] + this.grids[b] + this.grids[c];
        if (sum === 3) return this.winner = 1;
        if (sum === -3) return this.winner = -1;
        if ((sum === 1 || sum === -1) && this.grids.every((s) => s !== 0)) return this.winner = 3;
        // else return this.winner = 3;
        // if (this.grids !== [0, 0, 0, 0, 0, 0, 0, 0, 0]) return this.winner = 3;
      }
    },
  },
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
    border: 2px solid black;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
  }
}
</style>
