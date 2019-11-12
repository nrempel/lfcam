<template>
  <div id="app">
    <h1>DIY Plenoptic Camera</h1>
    <ImageLoader msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>

import ImageLoader from "./components/ImageLoader.vue";

export default {
  name: "app",
  components: {
    ImageLoader
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 3rem;
}
</style>
