<template>
  <header class="header">
    <img alt="Blue Orca logo" src="./assets/Orca_Updated_Logo.png" id='logo'>
  </header>
  
  <HelloWorld msg="Welcome to Blue Orca"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
}

#logo {
  max-width: 3rem;
}

.header {
  display: flex;
}
</style>
