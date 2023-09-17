<script setup>
  import Header from './components/Header.vue'
  import PhotoContainer from './components/PhotoContainer.vue'
</script>
<template>
<main>
  <div id="mainContainer">
  <Header></Header>
  <PhotoContainer />
  </div>
</main>

</template>

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
<style src="./assets/main.css"></style>