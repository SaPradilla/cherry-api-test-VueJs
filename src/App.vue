<script setup>
  import Login from './components/Login.vue';
  import Register from './components/Register.vue';
</script>

<template>
  <div class="md:flex  mt-10">
    <div class="md:w-1/2 md:h-screen">
      <h1 class="text-center text-4xl">Sing In</h1>
      <Login/>
    </div>
    <div class="md:w-1/2 md:h-screen">

      <h1 class="text-center text-4xl">Sign Up</h1>
      <Register/>
    </div>
  </div>
   
</template>

<style scoped>
</style>
