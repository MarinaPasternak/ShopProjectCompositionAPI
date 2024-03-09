<template>
  <header-component></header-component>
  <container-component></container-component>
</template>

<script setup>
import HeaderComponent from './components/HeaderComponent.vue';
import ContainerComponent from './components/ContainerComponent.vue';

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
