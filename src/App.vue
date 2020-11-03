<template>
  <div id="app">
    <VueObjectSlider/>
  </div>
</template>

<script>
import VueObjectSlider from './components/VueObjectSlider.vue'

export default {
  name: 'App',
  components: {
    VueObjectSlider
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
box-sizing: border-box;


  max-width: 1146px;
  margin: 60px auto;
}
body{
  margin: 0;
  padding: 0;
}
</style>
