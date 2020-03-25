<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <CalculateCli msg="Welcome to Online CLI calculator"/>
  </div>
</template>

<script>
import CalculateCli from './components/CalculateCli.vue'

export default {
  name: 'App',
  components: {
    CalculateCli
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
.logo {
  height: 250px;
}
</style>
