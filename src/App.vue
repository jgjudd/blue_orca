<template>
  <header class="header">
    <img alt="Blue Orca logo" src="./assets/Orca_Updated_Logo.png" id='logo'>
  </header>
  
  <HelloWorld msg="Welcome to Blue Orca"/>
  <Inflation />

</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Inflation from './components/Inflation.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    Inflation
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

@media (max-width: 600px) {
  .header {
    justify-content: center;
  }  
}

</style>
