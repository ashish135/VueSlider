<template>
  <div id="app">
       <Slider :itemsPerSlide="2" :autoplay="10000" :bulletPoint="true"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Slider from './components/Slider'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Slider
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
