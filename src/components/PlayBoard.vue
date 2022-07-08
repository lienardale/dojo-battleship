<template>
  <div>
    <p>{{ title }} {{ rowsCount }}x{{ columnsCount }} : {{ shouldDisplayShips }}</p>
  </div>
  <div class="playboard">
    <div class="title">{{ title }}</div>
    <div class="grid-container">
      <div class="line" v-for="column in columnsCount" :key="column">
		<div class='cell' :class="[ !boardCells['A1'] ? '' : shouldDisplayShips === false ? getCellStatus(row,column) + 'hidden' : getCellStatus(row,column) ]" v-for="row in rowsCount" :key="row">
           <!-- {{ row }} -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { getCell } from "../services/board-helper.js";
export default {
  name: "PlayBoard",
  props: {
    title: String,
    rowsCount: Number,
    columnsCount: Number,
    boardCells: {
      default: {},
      type: Object,
    },
	shouldDisplayShips: {
	  default: true,
	  type: Boolean
	},
  },
  methods: {
    getCellStatus(row, column) {
      return this.boardCells[getCell(row, column)].status
    }
  },
};
</script>

<style lang="scss" scoped>
.playboard {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.line {
  margin: 0px;
  width: fit-content;
  display: flex;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  & + & {
    border-top: none;
  }
}
.cell {
  border-left: 1px solid black;
  border-right: 1px solid black;
  & + & {
    border-left: none;
  }
  height: 3vw;
  width: 3vw;
}

.ship {
  background-color: black;
}
.ship.hidden {
  background-color: unset;
}
.missed {
  background-color: aqua;
}
.hit {
  background-color: yellow;
}
.sunk {
  background-color: red;
}
</style>
