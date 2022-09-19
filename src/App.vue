<template>
  <Navbar />
  <router-view/>
</template>

<script>
  import Navbar from '@/components/Navbar.vue'
export default {
  components: {
    Navbar
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
*{
  margin: 0;
  padding: 0;
  font-family: 'Lora', serif;
}
body{
  background-color: rgb(215, 236, 255);
}

</style>
