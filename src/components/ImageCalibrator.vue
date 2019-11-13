<template
  v-on:keyup.left="leftPressed"
  v-on:keyup.down="downPressed"
  v-on:keyup.right="rightPressed"
  v-on:keyup.up="upPressed"
>
  <div>
    <p>Calibrating 1 of {{ imageData.length }} images</p>
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
    // this.imagesWithOffsets[0] = {
    //   // initial image used as baseline
    //   imageData: this.images[0],
    //   offset: { dx: 0, dy: 0 }
    // };

    // new (Vue.extend(CalibratorImage))({
    //   propsData: { _src: this.images[this.currentImageIndex - 1], _style: {} }
    // }).mount("#calibration-zone");

    // const calibrationContainer = document.getElementById("calibration-zone");
    // // Draw last image to compare
    // const lastImage = document.createElement("img");
    // lastImage.src = this.images[this.currentImageIndex - 1];
    // lastImage.height = 400.0;
    // lastImage.style = `opacity: 0.25; position: absolute; top: 100px; left: 100px;`;
    // calibrationContainer.appendChild(lastImage);

    // // Draw current image to calibrate
    // currentImage = document.createElement("img");
    // this.currentImage.src = this.images[this.currentImageIndex];
    // this.currentImage.height = 400;
    // this.currentImage.style = `opacity: 0.25; position: absolute; top: 120px; left: 120px; border: 2px solid darkblue;`;
    // calibrationContainer.appendChild(this.currentImage);
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
    leftPressed() {
      console.log("leftPressed");
      this.dx--;
    },
    downPressed() {
      console.log("downPressed");
      this.dy--;
    },
    rightPressed() {
      console.log("rightPressed");
      this.dx++;
    },
    upPressed() {
      console.log("upPressed");
      this.dy++;
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
