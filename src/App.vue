<template>
  <div id="app">
    <AnimalList></AnimalList>
  </div>
</template>

<script>
import AnimalList from './components/AnimalList'

export default {
  name: 'App',
  components: {
AnimalList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
