<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <GoodsCar/>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import GoodsCar from './pages/GoodsCar.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    GoodsCar
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
ul,
li {
  list-style: none;
}
.btn {
  cursor: pointer;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
