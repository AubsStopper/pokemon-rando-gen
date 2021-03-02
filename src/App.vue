<template>
  <Header/>
  <PokemonRandomGen/>
</template>

<script>
import PokemonRandomGen from './components/PokemonRandomGen.vue'
import Header from './components/Header.vue'


export default {
  name: 'App',
  components: {
    Header,
    PokemonRandomGen
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

  display: grid;
  grid-template-rows: auto 1fr auto;
  width: 100%;
  

}

body {
  display: flex;
  margin: 0;
}
</style>
