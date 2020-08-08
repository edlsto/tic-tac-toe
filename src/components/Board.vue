<template>
  <div class="game">
    <div class="board">
      <Square
        v-for="(square, index) in board"
        :key="index"
        :id="index"
        :value="square"
        v-on:select="selectSquare"
      />
    </div>
    <ErrorMessage v-bind:error="this.error" />
  </div>
</template>

<script>
import Square from "./Square";
import ErrorMessage from "./ErrorMessage.vue";

import Vue from "vue";

export default {
  data() {
    return {
      board: [null, null, null, null, null, null, null, null, null],
      currentPlayer: 1,
      player1: "",
      player2: "",
      error: "",
    };
  },
  name: "Board",
  methods: {
    selectSquare: function(id) {
      if (!this.board[parseInt(id)]) {
        Vue.set(this.board, parseInt(id), this.currentPlayer === 1 ? "X" : "O");
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1;
        this.error = "";
      } else {
        this.error = "Tile already taken!";
      }
    },
    evaluateForWin: function(gameBoard, turn) {
      const playerSymbol = turn % 2 === 0 ? "X" : "O";
      const combinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
      ];
      return combinations.some((arr) => {
        return arr
          .map((el) => gameBoard[el])
          .every((el) => el === playerSymbol);
      });
    },
  },
  components: {
    Square,
    ErrorMessage,
  },
};
</script>

<style>
.board {
  display: flex;
  flex-wrap: wrap;
  width: 306px;
}
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
