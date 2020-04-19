<template>
  <div id="app">
    <h1>Hello World!</h1>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      API_KEY: process.env.VUE_APP_API_KEY,
    }
  },
}
</script>

<style lang="scss"></style>
