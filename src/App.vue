<template>
  <div id="app">
    <h1>Triangles</h1>
    <Output :a="a" :b="b" :c="c"></Output>
    <Sliders :a.sync="a" :b.sync="b" :c.sync="c"></Sliders>
  </div>
</template>

<script>
import Output from './Output.vue'
import Sliders from './Sliders.vue'

export default {
  name: 'app',
  data () {
    return {
      a: 150,
      b: 150,
      c: 150
    }
  },
  components: {
    Output,
    Sliders
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat');

* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Montserrat';
  font-weight: 100;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  h1 {
    font-size: 6em;
    font-weight: 100;
  }
}

</style>
