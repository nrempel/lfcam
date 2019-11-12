<template>
  <div id="app">
    <h1>DIY Plenoptic Camera</h1>
    <h2>Step 1: load your images</h2>
    <p>With large files this can take a minute so be patient.</p>
    <ImageLoader @image-loader-done="imageLoaderCallback" />
    <h2>Step 2: calibrate image offsets</h2>
  </div>
</template>

<script>
import ImageLoader from "./components/ImageLoader.vue";

export default {
  name: "app",
  components: {
    ImageLoader
  },
  methods: {
    imageLoaderCallback: function(binaryStrings) {
      console.log(binaryStrings);
    }
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
