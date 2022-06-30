<template>
  <div class="container-fluid mt-5">
    <Formulario  />
    <Tabla       />
  </div>
</template>

<script>
import Formulario from './componentes/Formulario.vue'
import Tabla from './componentes/Tabla.vue'

export default {
  name: 'App',
  components: {
    Formulario,
    Tabla
  },
}
</script>
