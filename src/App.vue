<template>
  <div id="app">
    <Compound msg="Calculate your compound interest" />
  </div>
</template>

<script>
import Compound from "./components/Compound.vue";

export default {
  name: "App",
  components: {
    Compound,
  },
};
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
