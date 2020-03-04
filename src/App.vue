<script>
import ComponentFactory from "@/componentComposer";
export default {
  name: "App",
  components: {
    ComponentFactory
  }
};
</script>

<template>
  <div id="app">
    <ComponentFactory name="Example" />
  </div>
</template>

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
