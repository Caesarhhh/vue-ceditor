<template>
  <div id="app">
    <vueCeditor></vueCeditor>
  </div>
</template>

<script>
  import TextInputArea from "./components/TextInputArea";
  import vueCeditor from "./components/vueCeditor";
export default {
  name: 'App',
  components:{
    vueCeditor:vueCeditor
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
