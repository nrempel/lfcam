<template>
  <div>
    <!-- <input type="file" value="Load Image" /> -->
    <div id="drop-target" @dragover.prevent @drop.prevent="loadImage">
      <span id="drop-target-title">Drop Images Here</span>
    </div>
    <div id="image-previews"></div>
  </div>
</template>

<script>
import Jimp from "jimp";
import { ArrayBufferToString } from "../util";
export default {
  name: "ImageLoader",
  props: {
    // callback: Function
  },
  methods: {
    loadImage: async function(e) {
      const binaryStrings = [];
      const files = e.dataTransfer.files;
      this.$emit("image-load-size", files.length);

      for (let i = 0; i < files.length; i++) {
        const file = files[i];
        const reader = new FileReader();

        reader.onloadend = e => {
          this.$emit("image-loaded", e.target.result);
        };

        reader.readAsDataURL(file);
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#drop-target {
  width: 200px;
  height: 100px;
  background-color: steelblue;
  border-width: 5px;
  border-color: thistle;
  border-style: solid;
  display: block;
}

#drop-target-title {
  width: 100%;
  line-height: 100%;
  display: inline-block;
  text-align: center;
  vertical-align: middle;
  margin: 0 auto;
  color: white;
  font-size: 1.2rem;
}
</style>
