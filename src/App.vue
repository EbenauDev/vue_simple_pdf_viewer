<template>
  <div id="app">
    <PDFViewer />
  </div>
</template>

<script>
import PDFViewer from "./components/PDFViewer";
export default {
  name: "App",
  components: {
    PDFViewer
  }
};
</script>

<style>
body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  position: relative;
  top: 0;
  left: 0;
  background-color: #1d3754;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 20px;
  padding: 0;
}
</style>
