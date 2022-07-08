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
	  IAAssets: {
        boardCells: {},
        boats: {},
	  },
    };
  },
  methods: {
    setAssets() {
      this.playerAssets = generateRandomAssets();
	  this.IAAssets = generateRandomAssets();
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
  <div class="board-container">
    <PlayBoard title="Player" :rowsCount="10" :columnsCount="10" :boardCells=playerAssets.boardCells :shouldDisplayShips="true" />
    <PlayBoard title="IA" :rowsCount="10" :columnsCount="10" :boardCells=IAAssets.boardCells :shouldDisplayShips="false" />
    <button @click="startGame()">startGame</button>
  </div>
  </div>
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

.boards-container {
  display: flex;
  justify-content: space-around;
  margin-bottom: 30px;
}

</style>
