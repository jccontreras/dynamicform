<template>
  <div id="app" class="container-fluid">
    <home/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

<script>
import Home from '@/views/Home.vue';

export default {
  components: {
    Home,
  },
};
</script>
