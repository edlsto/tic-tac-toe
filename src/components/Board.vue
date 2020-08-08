<template>
  <div class="board">
    <Square
      v-for="(square, index) in board"
      :key="index"
      :id="index"
      :value="square"
      v-on:select="selectSquare"
    />
  </div>
</template>

<script>
import Square from "./Square";
import Vue from "vue";

export default {
  data() {
    return {
      board: ["X", null, null, null, null, null, null, null, null],
    };
  },
  name: "Board",
  methods: {
    selectSquare: function(id) {
      console.log(id);

      Vue.set(this.board, parseInt(id), "X");
    },
  },
  components: {
    Square,
  },
};
</script>

<style>
.board {
  display: flex;
  flex-wrap: wrap;
  width: 306px;
}
</style>
