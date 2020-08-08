<template>
  <div class="game">
    <div v-if="player1">
      <div>Player 1</div>
      <div>{{ player1 }}</div>
    </div>
    <div v-if="player2">
      <div>Player 2</div>
      <div>{{ player2 }}</div>
    </div>

    <div class="player-input" v-if="!player1 || !player2">
      <label for="input" v-if="!player1">Player 1</label>
      <label for="input" v-else>Player 2</label>
      <input
        type="text"
        v-model="input"
        id="input"
        v-on:keyup.enter="addPlayer"
      />
    </div>

    <div class="board">
      <Square
        v-for="(square, index) in board"
        :key="index"
        :id="index"
        :value="square"
        v-on:select="selectSquare"
      />
    </div>
    <Message v-bind:message="this.message" />
  </div>
</template>

<script>
import Square from "./Square";
import Message from "./Message.vue";

import Vue from "vue";

export default {
  data() {
    return {
      board: [null, null, null, null, null, null, null, null, null],
      currentPlayer: 1,
      player1: "",
      player2: "",
      input: "",
      message: "",
      gameOver: false,
    };
  },
  name: "Board",
  methods: {
    selectSquare: function(id) {
      if (this.gameOver) {
        return;
      } else if (!this.board[parseInt(id)]) {
        Vue.set(this.board, parseInt(id), this.currentPlayer === 1 ? "X" : "O");
        this.evaluateForWin(this.board);
      } else {
        this.message = "Tile already taken!";
      }
    },
    evaluateForWin: function(gameBoard) {
      const playerSymbol = this.currentPlayer === 1 ? "X" : "O";
      console.log(playerSymbol);
      const combinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
      ];
      const result = combinations.some((arr) => {
        return arr
          .map((el) => gameBoard[el])
          .every((el) => el === playerSymbol);
      });
      if (result) {
        this.message = `${
          this.currentPlayer === 1 ? this.player1 : this.player2
        } won!`;
        this.gameOver = true;
        return;
      } else {
        this.currentPlayer = this.currentPlayer === 1 ? 2 : 1;
        this.message = "";
      }
    },
    addPlayer: function() {
      if (!this.player1) {
        this.player1 = this.input;
        this.input = "";
      } else {
        this.player2 = this.input;
        this.input = "";
      }
    },
  },
  components: {
    Square,
    Message,
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
.player-input {
  margin-bottom: 1em;
}
</style>
