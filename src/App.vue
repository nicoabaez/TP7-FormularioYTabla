<template>
  <div class="container-fluid mt-5">
    <Navbar  />
    <router-view />
  </div>
</template>

<script>
import Navbar from '/src/componentes/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar
  },
}
</script>
