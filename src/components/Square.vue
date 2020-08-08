<template>
  <div class="square" v-on:click="handleSelect">
    {{ value }}
  </div></template
>

<script>
export default {
  name: "Square",
  props: ["id", "value"],
  methods: {
    handleSelect: function() {
      this.$emit("select", this.$props.id);
    },
  },
};
</script>

<style>
.square {
  width: 100px;
  height: 100px;
  border: 1px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3em;
  cursor: pointer;
}
</style>
