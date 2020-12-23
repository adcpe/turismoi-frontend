<template>
  <div id="app">
    <Tour />
  </div>
</template>

<script>
import Tour from './components/Tour.vue';

export default {
  name: 'App',
  components: {
    Tour,
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
