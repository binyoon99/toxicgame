<script setup>
  import Header from './components/Header.vue'
  import PhotoContainer from './components/PhotoContainer.vue'
  import InputContainer from './components/InputContainer.vue';
</script>
<template>
<main>
  <Header></Header>
  <PhotoContainer />
  <InputContainer />
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