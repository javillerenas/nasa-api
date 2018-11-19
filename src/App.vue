<template>
  <div id="app">
    <NasaAsteroids></NasaAsteroids>
    <NasaApod></NasaApod>
  </div>
</template>

<script>
import NasaApod from './components/NasaApod.vue'
import NasaAsteroids from './components/NasaAsteroids.vue'

export default {
  name: 'app',
  components: {
    NasaApod,
    NasaAsteroids
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
</style>
