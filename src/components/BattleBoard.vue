<script>
import PlayBoard from "./PlayBoard.vue";
import { generateRandomAssets } from "../services/board-helper.js";
export default {
  name: "BattleBoard",
  components: { PlayBoard },
  data() {
    return {
      playerAssets: {
        boardCells: {},
        boats: {},
      },
      gameStarted: false,
    };
  },
  methods: {
    setAssets() {
      this.playerAssets = generateRandomAssets();
    },
    startGame(event) {
      this.setAssets();
      console.log(this.playerAssets)
    },
  },
};
</script>

<template>
  <div class="battle-board">
    <div class="title">Battleship</div>
  </div>
  <PlayBoard title="Player" :rowsCount="10" :columnsCount="10" :boardCells=playerAssets.boardCells />
  <button @click="startGame()">startGame</button>
</template>

<style lang="scss" scoped>
.title {
  font-size: 30px;
  font-weight: bold;
  margin-bottom: 30px;
}
.battle-board {
  padding: 30px;
}
</style>
