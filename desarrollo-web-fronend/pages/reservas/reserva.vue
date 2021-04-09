<template>

<v-container >
    <div style="margin-top:2%">
    <h3>Formulario para registrar reservas</h3>
    
<v-form ref="formularioReserva" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="reserva.id"
            :rules="regla.obligatorio"
            label="Id"
            required
            clearable
          ></v-text-field>
          <v-text-field
            v-model="reserva.usuario"
            :rules="regla.obligatorio"
            label="reservante"
            required
            clearable
          ></v-text-field>
 <v-text-field
            v-model="reserva.instalacion"
            :rules="regla.obligatorio"
            label="instalacion"
            required
            clearable
          ></v-text-field>
  <v-text-field
            v-model="reserva.fecha"
            :rules="regla.obligatorio"
            label="fecha"
            required
            clearable
          ></v-text-field>     
  <v-text-field
            v-model="reserva.personasn"
            :rules="regla.obligatorio"
            label="numero de personas"
            required
            clearable
          ></v-text-field>            
 

          
          <v-row
          width="100px">
          <v-col>
 <v-btn
            
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/reservas"
            rounded
            >
            Mostrar reservas
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
      reserva:{id:"",usuario:"",instalacion:"",fecha:"",personasn:""},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){},
   methods: {
     async agregar () {
          if (this.$refs.formularioReserva.validate()) {
              let reserva=Object.assign({},this.reserva);
            let response= await this.$axios.post('http://localhost:3001/reservas',reserva);
            this.$swal("agregado");  
          }
          else{
            console.log("mal ");
          }      
      },

     
      async getreserva()
      {
         let response= await this.$axios.get('http://localhost:3001/reservas')
            console.log(response);
      }


    },
    }

</script>
