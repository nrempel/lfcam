<template>
  <div>
    <label for="depth"
      >image depth
      <input v-model="sliderValue" @input="changeDepth" type="range" id="depth" min="1" max="400" value="200" step="0.5" />
    </label>
    <br/>
    <div id="image-wrapper">
      <div v-for="(imageState, key) in imageStates" :key="key">
        <img
          height="450"
          v-bind:style="{
            top: `${imageState.dy}px`,
            left: `${imageState.dx - fromCenter * key}px`
          }"
          v-bind:src="imageState.data"
        />
      </div>
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
      imageStates: this.imageData,
      sliderValue: 200,
      fromCenter: 0
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
    // const imageStates = {};
    // for (let i = 0; i < this.imageData.length; i++) {
    //   const image = this.imageData[i];
    //   imageStates[i] = {};
    //   imageStates[i]["data"] = image;
    //   imageStates[i]["visible"] = false;
    //   imageStates[i]["dx"] = 50 + 10 * i;
    //   imageStates[i]["dy"] = 50 + 10 * i;
    // }
    // imageStates[0]["visible"] = true;
    // this.imageStates = imageStates;
  },
  methods: {
    changeDepth() {
      // [200, 200]
      this.fromCenter = 200 - this.sliderValue
    }
  }
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

#image-wrapper {
  position: relative;
  margin-left:5rem;
  margin-bottom: 20rem;
}

input {
  width: 300px;
  margin-bottom: 2rem;
}
</style>
