<template>
  <div id="app">
    <SampleForm/>
  </div>
</template>

<script>
import SampleForm from './components/SampleForm.vue'

export default {
  name: 'App',
  components: {
    SampleForm
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
