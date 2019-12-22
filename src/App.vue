<template>
  <b-container fluid id="app">
    <NavBar msg="Welcome to Your Vue.js App"/>
    <Arena></Arena>
    <p v-if="hero"> YES</p>
  </b-container>
</template>

<script>
import NavBar from './components/NavBar.vue';
import Arena from './components/Arena.vue';

export default {
  name: 'app',
  components: {
    NavBar, Arena
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
