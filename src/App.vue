<template>

  <Header/>
  <Body msg="Welcome to Your Vue.js App"/>

</template>

<script>
import Body from './components/Body.vue'
import Header from './components/Header.vue'


export default {
  name: 'App',
  components: {
    Body,
    Header
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

  display: flex;
  justify-content: center;
  width: 100%;
  margin: 0;

}

body {
  height: 100vh;
  display: flex;

}
</style>
