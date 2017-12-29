<template>
  <div>
    <div class="textContainer">{{ a }}</div>
    <div class="sliderContainer"><input ref="sliderA" class="slider" type="range" v-bind:min="aMin" v-bind:max="aMax" @change="updateA"></div>
    <div class="textContainer">{{ b }}</div>
    <div class="sliderContainer"><input ref="sliderB" class="slider" type="range" v-bind:min="bMin" v-bind:max="bMax" @change="updateB"></div>
    <div class="textContainer">{{ c }}</div>
    <div class="sliderContainer"><input ref="sliderC" class="slider" type="range" v-bind:min="cMin" v-bind:max="cMax" @change="updateC"></div>
  </div>
</template>

<script>
module.exports = {
  props: ["a", "b", "c"],
  computed: {
    aMax: function() {
      return this.b + this.c - 1
    },
    aMin: function() {
      return Math.max(Math.abs(this.b - this.c), 1)
    },
    bMax: function() {
      return this.a + this.c - 1
    },
    bMin: function() {
      return Math.max(Math.abs(this.a - this.c), 1)
    },
    cMax: function() {
      return this.a + this.b - 1
    },
    cMin: function() {
      return Math.max(Math.abs(this.a - this.b), 1)
    },
  },
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
    height: 45px;
    width: 20px;
    /* border-radius: 50%; */
    border-radius: 3px;
    background: goldenrod;
    margin-top: -15px;
  }

  input[type=range]:focus {
    outline: none;
  }

  input[type=range]:focus::-webkit-slider-runnable-track {
    background: #ccc;
  }
</style>