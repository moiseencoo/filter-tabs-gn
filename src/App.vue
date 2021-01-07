<template>
  <div id="app">
    <filter-tabs></filter-tabs>
  </div>
</template>

<script>
import FilterTabs from './components/FilterTabs.vue'

export default {
  name: 'App',
  components: {
    FilterTabs
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
  margin-top: 60px;
}
</style>
