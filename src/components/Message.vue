<template>
  <div class="message">
    {{ message }}
  </div>
</template>

<script>
export default {
  name: "Message",
  props: ["message"],
};
</script>

<style>
.message {
  margin-top: 2em;
}
</style>
