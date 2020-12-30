<template>
  <div id="app" class="container-fluid d-flex justify-content-center align-items-center">
    <FormInput />
  </div>
</template>

<script>
import FormInput from './components/FormInput.vue';

export default {
  name: 'App',
  components: {
    FormInput, 
  }
}
</script>

<style >
@font-face {
  font-family: "Merienda";
  src: local("Merienda"),
   url(./assets/fonts/GT-America-Regular.otf) format("truetype");
}
#app {
  font-family: "GT America", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #292827;
  height:100vh;
  max-width:100vw
}
</style>
