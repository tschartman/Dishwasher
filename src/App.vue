<template>
  <div id="app">
    <Dishwasher/>
  </div>
</template>

<script>
import Dishwasher from './components/Dishwasher.vue'

export default {
  name: 'App',
  components: {
    Dishwasher
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
