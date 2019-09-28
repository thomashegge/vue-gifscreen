<template>
  <div class="footer__content">
    <input type="text" v-bind:value="value" v-on:keydown="$emit('input', $event)" :placeholder="label">
    <span>or</span>
    <button v-on:click="$emit('bySong')">Song playing</button>
    <span>or</span>
    <button v-on:click="$emit('tryLuck')">Try my luck</button>
  </div>
</template>

<script>
export default {
  name: 'Search',
  props: {
    label: String,
    value: String,
  },
}
</script>

<style scoped>
  form {
    margin: 75px 0;
  }
  input {
    font-size: 20px;
    padding: 5px;
    min-width: 300px;
  }

  span, button {
    margin-left: 28px;
  }
</style>
