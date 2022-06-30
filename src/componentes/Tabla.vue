<template>

  <section class="src-componentes-tabla">
    <div class="jumbotron">
       <br>
      <label><h2>Tabla de Usuarios</h2></label>
      <br>

      <div v-if="usuarios.length" class="table-responsive">
        <table class="table">
          <tr>
            <th>Nombre</th>
            <th>Edad</th>
            <th>Email</th>
          </tr>
          <tr v-for="(usuarioRecorrido, index) in usuarios" :key="index">
            <td>{{  usuarioRecorrido.nombre  }}</td>
            <td>{{  usuarioRecorrido.edad    }}</td>
            <td>{{  usuarioRecorrido.email    }}</td>
          </tr>
        </table>
      </div>
      <h3 v-else class="alert alert-danger"> No hay usuarios disponibles.</h3>
    </div>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'src-componentes-tabla',
    props: [],
    mounted () {
      this.getUsuarios()
    },
    data () {
      return {
        url:      'https://6286f9227864d2883e7c4e53.mockapi.io/usuarios2/',
        usuarios: []
      }
    },
    methods: {
    async getUsuarios() {
      /* -------------------- */
      /* axios con then/catch */
      this.axios(this.url)
        .then(({ data:respuesta }) => {
          this.usuarios = respuesta
        })
        .catch( error => console.error('Error en Axios:', error))
      // try {
      //   let {data:usuarios} = await this.axios(this.url)
      //   this.usuarios = usuarios
      // }
      // catch(error) {
      //   console.error('Error en getUsuarios', error.message)
      // }
      }
    },
  }


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: rgba(56, 23, 116, 0.589);
  }
</style>
