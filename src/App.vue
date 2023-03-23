<template>
  <ConvCalculator />
</template>

<script>
import ConvCalculator from './components/conversionTable.vue'

export default {
  name: 'App',
  components: {
    ConvCalculator
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
