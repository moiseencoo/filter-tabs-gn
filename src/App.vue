<template>
  <div id="app">

    <el-queue></el-queue>
  </div>
</template>

<script>
import ElQueue from './components/ElQueue.vue'

export default {
  name: 'App',
  components: {
    ElQueue
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
