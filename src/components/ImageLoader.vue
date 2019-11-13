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
    render: function(src) {
      var image = new Image();
      var MAX_HEIGHT = 1000;
      image.onload = function() {
        var canvas = document.getElementById("canvas");
        if (image.height > MAX_HEIGHT) {
          image.width *= MAX_HEIGHT / image.height;
          image.height = MAX_HEIGHT;
        }
        var ctx = canvas.getContext("2d");
        // ctx.clearRect(0, 0, canvas.width, canvas.height);
        // canvas.width = image.width;
        // canvas.height = image.height;
        ctx.drawImage(image, 0, 0, image.width, image.height);
      };
      image.src = src;
    },
    renderPreview: function(buf) {
      // var imageElem = document.createElement("img");
      // imageElem.src = "data:image/jpeg;base64," + buf.toString("base64");
      // var container = document.getElementById("image-previews");
      // container.appendChild(imageElem)
      const span = document.createElement("span");
      span.textContent = `${12} images loaded`;
      // var container = document.getElementById("image-previews");
      // container.appendChild(imageElem)
    },
    loadImage: async function(e) {
      // reader.onload = e => {
      //   this.render(e.target.result);
      // };

      const binaryStrings = [];
      const files = e.dataTransfer.files;
      this.$emit("image-load-size", files.length);

      for (let i = 0; i < files.length; i++) {
        const file = files[i];
        const reader = new FileReader();
        // const promise = new Promise((resolve, reject) => {
          reader.onloadend = e => {
            this.$emit("image-loaded", e.target.result);
            // resolve(e.target.result);
          };
        // });
        reader.readAsDataURL(file);
        
        // const imageData = await promise;
        console.log("image data read");
        // this.$emit("image-loaded", imageData);
      }

      // files.forEach(file => reader.readAsDataURL(file));
    },
    loadPreviews: function(binaryStrings) {
      binaryStrings.forEach(str => {
        Jimp.read(str).then(image => {
          image.resize(Jimp.AUTO, 100);
          image.getBufferAsync(Jimp.MIME_PNG).then(this.renderPreview);
        });
      });
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

#canvas {
  margin-top: 2rem;
  border: 5px solid black;
  width: 1000px;
  height: 350px;
}
</style>
