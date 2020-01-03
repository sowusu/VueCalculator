<template>
  <div id="app">
    <h1><span><img src="./assets/logo.png"></span>ue Calculator </h1>
    <Calculator></Calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'app',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  font-size: 3em;
}

img{
  max-width: 50px;
  max-height: 80px;
  height: 80px;
}
</style>
