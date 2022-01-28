<template>
  
  <div id="app">
   <img class="logo" alt="Vue logo" src="./assets/logo.png">
   <toDo></toDo>
  </div>

</template>

<script>
import toDo from './components/toDo.vue'


export default {
  name: 'App',
  components: {
    toDo,
  }
}

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Irish+Grover&family=Poppins:ital,wght@1,100&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 20px;
  margin: 0;
  padding: 0;
  
}

* {
  box-sizing: border-box;  
  margin: 0;
  padding: 0;
}


.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}






</style>
