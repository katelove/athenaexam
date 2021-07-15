<template>
  <div id="app">
    <!-- <img src="./assets/logo.png" /> -->
    <GradesSystem />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
import GradesSystem from "./components/GradesSystem.vue";
export default {
  name: "App",
  components: {
    GradesSystem,
    // HelloWorld
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
