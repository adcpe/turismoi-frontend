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
  margin: 0 auto;
  width: 80%;

}

@media screen and (max-width: 768px) {
  #app {
    width: 100%;
  }
}
</style>
