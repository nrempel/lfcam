<template>
  <img v-bind:src="src" v-bind:style="style" />
</template>

<script>
export default {
  name: "CalibratorImage",
  props: {
    _style: Object,
    _src: String
  }
  //   computed: {
  //     style() {
  //       return this.styleObject;
  //     }
  //   }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
