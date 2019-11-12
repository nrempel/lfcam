<template>
  <div>
    <!-- <input type="file" value="Load Image" /> -->
    <div id="drop-target" @dragover.prevent @drop.prevent="loadImage">
      <span id="drop-target-title">Drop Images Here</span>
    </div>
    <canvas id="canvas"></canvas>
  </div>
</template>

<script>
export default {
  name: "ImageLoader",
  props: {
    msg: String
  },
  methods: {
    render: function(src) {
      var image = new Image();
      var MAX_HEIGHT = 10;
      image.onload = function() {
        var canvas = document.getElementById("canvas");
        if (image.height > MAX_HEIGHT) {
          image.width *= MAX_HEIGHT / image.height;
          image.height = MAX_HEIGHT;
        }
        var ctx = canvas.getContext("2d");
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        canvas.width = image.width;
        canvas.height = image.height;
        ctx.drawImage(image, 0, 0, image.width, image.height);
      };
      image.src = src;
    },
    loadImage: function(e) {
      var reader = new FileReader();
      reader.onload = e => {
        this.render(e.target.result);
      };

      const files = e.dataTransfer.files;
      console.log(files);

      files.forEach(file => reader.readAsDataURL(file));
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
  background-color: aliceblue;
  width: 1000px;
  height: 350px;
}
</style>
