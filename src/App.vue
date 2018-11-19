<template>
  <div id="app">
    <Greeter name="javi"></Greeter>
    <NasaAsteroids></NasaAsteroids>
    <NasaApod></NasaApod>
  </div>
</template>

<script>
import Greeter from './components/Greeter.vue'
import NasaApod from './components/NasaApod.vue'
import NasaAsteroids from './components/NasaAsteroids.vue'

export default {
  name: 'app',
  components: {
    Greeter,
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
