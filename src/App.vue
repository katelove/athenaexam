
<template>
  <div id="app">
    <GradesSystem />
  </div>
</template>

<script>
// eslint-disable-next-line
import GradesSystem from "./components/GradesSystem.vue";
export default {
  // eslint-disable-next-line
  name: "App",
  components: {
    // eslint-disable-next-line
    GradesSystem,
    // eslint-disable-next-line
  },
  // eslint-disable-next-line
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
