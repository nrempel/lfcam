<template>
  <div>
    <p>Calibrating 1 of {{ images.length }} images</p>

    <div id="calibration-zone"></div>
  </div>
</template>

<script>
import { ArrayBufferToString } from "../util";
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
      currentImageIndex: 1,
      imagesWithOffsets: {}
    };
  },
  mounted: function() {
    this.imagesWithOffsets[0] = {
      // initial image used as baseline
      imageData: this.images[0],
      offset: { dx: 0, dy: 0 }
    };

    const calibrationContainer = document.getElementById("calibration-zone");
    // Draw last image to compare
    const lastImage = document.createElement("img");
    lastImage.src = this.images[this.currentImageIndex - 1];
    lastImage.height = 400.0;
    lastImage.style = `opacity: 0.25; position: absolute; top: 100px; left: 100px;`;
    calibrationContainer.appendChild(lastImage);

    // Draw current image to calibrate
    const thisImage = document.createElement("img");
    thisImage.src = this.images[this.currentImageIndex];
    thisImage.height = 400;
    thisImage.style = `opacity: 0.25; position: absolute; top: 120px; left: 120px; border: 2px solid darkblue;`;
    calibrationContainer.appendChild(thisImage);
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#calibration-zone {
  position: relative;
  border: 1px solid black;
  width: 100%;
  height: 1000px;
}
</style>
