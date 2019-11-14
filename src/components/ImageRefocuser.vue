<template>
  <div
    id="calibration-zone"
    v-bind:style="{
      width: imageLocked ? 'auto' : '100%',
      height: imageLocked ? 'auto' : '600px',
      border: imageLocked ? 'none' : '1px solid black'
    }"
  >
    <div v-for="(imageState, key) in imageStates" :key="key">
      <img
        height="400"
        v-show="imageState.visible"
        v-bind:style="{
          top: `${imageState.dy}px`,
          left: `${imageState.dx}px`
        }"
        v-bind:src="imageState.data"
      />
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  name: "ImageRefocuser",
  props: {
    imageData: Array
  },

  data: function() {
    return {
      imageStates: this.imageStates
    };
  },
  mounted: function() {
    window.addEventListener("keydown", e => {
      switch (e.keyCode) {
        case 37:
          this.leftPressed(e.shiftKey);
          return false;
          break;
        case 38:
          this.upPressed(e.shiftKey);
          return false;
          break;
        case 39:
          this.rightPressed(e.shiftKey);
          return false;
          break;
        case 40:
          this.downPressed(e.shiftKey);
          return false;
          break;

        default:
          break;
      }
      return false;
    });
  },
  created: function() {
    const imageStates = {};
    for (let i = 0; i < this.imageData.length; i++) {
      const image = this.imageData[i];
      imageStates[i] = {};
      imageStates[i]["data"] = image;
      imageStates[i]["visible"] = false;
      imageStates[i]["dx"] = 50 + 10 * i;
      imageStates[i]["dy"] = 50 + 10 * i;
    }
    imageStates[0]["visible"] = true;
    this.imageStates = imageStates;
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  position: absolute;
  opacity: 0.25;
  box-sizing: content-box;
}

.button {
  font-size: 1rem;
  margin-bottom: 2rem;
  margin-right: 1rem;
}
</style>
