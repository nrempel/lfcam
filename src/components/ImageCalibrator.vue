<template v-on:keydown="keyDown">
  <div>
    <p>
      Calibrating {{ currentImageIndex + 1 }} of {{ imageData.length }} images
    </p>
    <button class="button" v-on:click="prevImage">previous image</button>
    <button class="button" v-on:click="nextImage">next image</button>
    <div id="calibration-zone">
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
  </div>
</template>

<script>
import CalibratorImage from "./CalibratorImage.vue";
import Vue from "vue";
export default {
  name: "ImageCalibrator",
  props: {
    imageData: Array
  },
  computed: {
    images() {
      return this.imageData;
    }
  },
  data: function() {
    return {
      // images: this.imageArray,
      currentImageIndex: 0,
      imageStates: null
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
  methods: {
    nextImage() {
      if (this.currentImageIndex == this.imageData.length - 1) {
        return;
      }
      this.currentImageIndex++;
      this.imageStates[this.currentImageIndex]["visible"] = true;
    },
    prevImage() {
      if (this.currentImageIndex <= 0) {
        return;
      }
      this.imageStates[this.currentImageIndex]["visible"] = false;
      this.currentImageIndex--;
    },
    leftPressed(shift) {
      const delta = shift ? 10 : 1;
      this.imageStates[this.currentImageIndex]["dx"] -= delta;
    },
    downPressed(shift) {
      const delta = shift ? 10 : 1;
      this.imageStates[this.currentImageIndex]["dy"] += delta;
    },
    rightPressed(shift) {
      console.log("rightPressed");
      const delta = shift ? 10 : 1;
      this.imageStates[this.currentImageIndex]["dx"] += delta;
    },
    upPressed(shift) {
      console.log("upPressed");
      const delta = shift ? 10 : 1;
      this.imageStates[this.currentImageIndex]["dy"] -= delta;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#calibration-zone {
  position: relative;
  border: 1px solid black;
  width: 100%;
  height: 600px;
}

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
