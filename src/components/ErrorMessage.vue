<template>
  <div class="error-message">
    {{ error }}
  </div>
</template>

<script>
export default {
  name: "ErrorMessage",
  props: ["error"],
};
</script>

<style>
.error-message {
  margin-top: 2em;
}
</style>
