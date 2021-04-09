<template>

<v-container >
    <div style="margin-top:2%">
    <h3>Editar instalaciones</h3>
    <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/instalaciones"
            rounded
            >
            ver registro
            </v-btn>
<v-form ref="formularioinstalaciones" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="instalacion.id"
            :rules="regla.obligatorio"
            label="Id"
            required
          ></v-text-field>
          <v-text-field
            v-model="instalacion.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
          ></v-text-field>
 <v-text-field
            v-model="instalacion.precio"
            :rules="regla.obligatorio"
            label="Precio"
            required
          ></v-text-field>


          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            @click="editar()"
            rounded
            >
            editar instalacion
            </v-btn>
          </v-col>

                        
</v-row>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
  async asyncData({ params }) {
      let id_instalacion=params.id;
      return {id_instalacion}
    },
   data: () => ({
      valid: true,
      instalacion:{},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){
      this.getinstalacion();
    },
   methods: {
      async getinstalacion()
      {
          try {
               let response= await this.$axios.get('http://localhost:3001/instalaciones/' + this.id_instalacion );
            console.log(response);
            this.instalacion=response.data
          } catch (error) {
             this.$swal(" error");
          }
        
      },
    
      async editar () {
        if (this.$refs.formularioinstalaciones.validate()) {
              let instalacion=Object.assign({},this.instalacion);
            let response= await this.$axios.put('http://localhost:3001/instalaciones/' + this.id_instalacion,instalacion);
            console.log(response +"respuesta");
            this.$swal("se realizo con exito");
          }
          else{
            console.log("mal");
          }      
      },
      
      actualizar () {
        this.$refs.form.resetValidation()
      },
     


    },
    }

</script>
