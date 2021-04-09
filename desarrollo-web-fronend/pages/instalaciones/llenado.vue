<template>

<v-container >
    <div style="margin-top:2%">
    <h3>Formulario para registrar instalaciones</h3>
    
<v-form ref="formularioinstalaciones" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="instalacion.id"
            :rules="regla.obligatorio"
            label="Id"
            required
            clearable
          ></v-text-field>
          <v-text-field
            v-model="instalacion.nombre"
            :rules="regla.obligatorio"
            label="Nombre"
            required
            clearable
          ></v-text-field>
 <v-text-field
            v-model="instalacion.precio"
            :rules="regla.obligatorio"
            label="precio"
            required
            clearable
          ></v-text-field>
 

          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/instalaciones"
            rounded
            >
            Mostrar instalaciones
            </v-btn>
          </v-col>
<v-fab-transition>
              <v-btn
                color="rgb(30, 181,181, 0.9)"
                dark
                absolute
                
                bottom
                right
                fab
                @click="agregar()"
              >
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-fab-transition>
                        
</v-row>
</v-form>
</div>
 
</v-container>

</template>



<script>

export default {
  
   data: () => ({
      valid: true,
      instalacion:{id:"",nombre:"",precio:""},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){},
   methods: {
     async agregar () {
          if (this.$refs.formularioinstalaciones.validate()) {
              let instalacion=Object.assign({},this.instalacion);
            let response= await this.$axios.post('http://localhost:3001/instalaciones',instalacion);
            this.$swal("agregado");  
          }
          else{
            console.log("mal ");
          }      
      },

     
      async getinstalacion()
      {
         let response= await this.$axios.get('http://localhost:3001/instalaciones')
            console.log(response);
      }


    },
    }

</script>
