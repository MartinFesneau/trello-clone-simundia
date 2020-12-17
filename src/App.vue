<template>
  <the-board></the-board>
</template>

<script>
  import TheBoard from './components/TheBoard'

export default {
  name: 'App',
  components: {
    TheBoard,
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
body {
  background-color: #F9FAFC;
}
</style>
