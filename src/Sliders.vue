<template>
  <div>
    <div class="textContainer">{{ a }}</div>
    <div class="sliderContainer"><input ref="sliderA" class="slider" type="range" min="1" max="10" @input="updateA"></div>
    <div class="textContainer">{{ b }}</div>
    <div class="sliderContainer"><input ref="sliderB" class="slider" type="range" min="1" max="10" @input="updateB"></div>
    <div class="textContainer">{{ c }}</div>
    <div class="sliderContainer"><input ref="sliderC" class="slider" type="range" min="1" max="10" @input="updateC"></div>
  </div>
</template>

<script>
module.exports = {
  props: ["a", "b", "c"],
  methods: {
    updateA: function() {
      this.$emit("update:a", parseInt(this.$refs.sliderA.value))
    },
    updateB: function() {
      this.$emit("update:b", parseInt(this.$refs.sliderB.value))
    },
    updateC: function() {
      this.$emit("update:c", parseInt(this.$refs.sliderC.value))
    }
  },
  mounted: function() {
    this.$refs.sliderA.value = this.a
    this.$refs.sliderB.value = this.b
    this.$refs.sliderC.value = this.c
  }
}
</script>

<style scoped>
  .textContainer {
    font-size: 2em;
  }

  .sliderContainer {
    margin: 0 100px;
  }

  input[type=range] {
    -webkit-appearance: none;
    margin-bottom: 100px;
    height: 30px;
    width: 100%;
    margin-top: 10px;
  }

  input[type=range]::-webkit-slider-runnable-track {
    width: 300px;
    height: 15px;
    background: #ddd;
    border: none;
    border-radius: 3px;
  }

  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    border: none;
    height: 55px;
    width: 55px;
    border-radius: 50%;
    background: goldenrod;
    margin-top: -20px;
  }

  input[type=range]:focus {
    outline: none;
  }

  input[type=range]:focus::-webkit-slider-runnable-track {
    background: #ccc;
  }
</style>