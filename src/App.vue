<template>
  <div id="app">
    <life-component/>
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
  </div>
</template>

<script>

import LifeComponent from "@/components/LifeComponent";
export default {
  name: 'App',
  components: {
    LifeComponent
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
  display: flex;
  justify-content: center;
}
</style>
