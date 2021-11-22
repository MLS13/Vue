<template>
  <PrevisaoTempo/>
</template>

<script>
import PrevisaoTempo from './components/PrevisaoTempo.vue'

export default {
  name: 'App',
  components: {
    PrevisaoTempo
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Poppins&display=swap");
#app {
  font-family: 'Poppins', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

html{
  background-color: #6377EE;
}
</style>
