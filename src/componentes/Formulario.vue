<template>

  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <vue-form :state="formState" @submit.prevent="enviar()">
      
      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="nombre">Nombre</label>
        <input
          type="text"
          id="nombre"
          class="form-control"
          name="nombre" 
          autocomplete="off"
          v-model.trim="formData.nombre"
          required 
          :minlength="minNombre"
          :maxlength="maxNombre"
          no-espacios
        />
  
        <field-messages name="nombre" show="$dirty">
          <div slot="required"    class="alert alert-danger mt-1"> Campo requerido</div>
          <div slot="minlength"   class="alert alert-danger mt-1"> Minimo {{minNombre}} caracteres</div>
          <div slot="no-espacios" class="alert alert-danger mt-1"> No se pueden colocar espacios intermedios </div>
        </field-messages>
      </validate>

      <br>

      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="edad">Edad</label>
        <input
          type="number"
          id="edad"
          class="form-control"
          name="edad" 
          autocomplete="off"
          v-model.number="formData.edad"
          required
          :min="edadMin"
          :max="edadMax"
        />
  
        <field-messages name="edad" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
          <div slot="min"      class="alert alert-danger mt-1">Edad mínima {{edadMin}}</div>
          <div slot="max"      class="alert alert-danger mt-1">Edad fuera de rango {{edadMax}}</div>
        </field-messages>
      </validate>

      <br>

      <!--CAMPO Y VALIDACIONES-->

      <validate tag="div">
        <label for="email">Email</label>
        <input
          type="email"
          id="email"
          class="form-control"
          name="email" 
          autocomplete="off"
          v-model="formData.email"
          required 
        />
  
        <field-messages name="email" show="$dirty">
          <div slot="required" class="alert alert-danger mt-1">Campo requerido</div>
        </field-messages>
      </validate>

      <br>
  
      <button class="btn btn-success my-3" :disabled="formState.$invalid">ENVIAR</button>
    </vue-form>
    </div>
  </section>

</template>

<script lang="js">

  export default  {
    name: 'src-componentes-formulario',
    props: [],
    mounted () {
    },
    data () {
      return {
        formState: {

        },
        formData: this.getInitialData(),
        edadMin: 18,
        edadMax: 120,
        minNombre: 3,
        maxNombre: 15,
        url: 'https://6286f9227864d2883e7c4e53.mockapi.io/usuarios2/',      
      }
    },
    methods: {
      getInitialData(){
        return {
          nombre:   null,
          edad:     null,
          email:    null,
        }
      },
      async enviar(){
        try {
          let usuarioIngresado = {...this.formData}
          await this.axios.post(this.url, usuarioIngresado, {'content-type':'application/json'} )
        }
        catch(error) {
          console.error('Error en postUsuario', error.message)
        }
        this.formData = this.getInitialData()
        this.formState._reset()
        // location.reload();
      },
    },
    computed: {

    }
}


</script>

<style scoped lang="css">
  .jumbotron{
    background-color: rgb(55, 23, 116);
  }
  label{
    color: white
  }
</style>
