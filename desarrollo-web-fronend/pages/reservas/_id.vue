<template>

<v-container >
    <div style="margin-top:2%">
    <h3>Edicion de reservas</h3>
    <v-btn
            :disabled="!valid"
            color="rgb(30, 181,181, 0.3)"
            class="text-none"
            to="/reservas"
            rounded
            >
            ver registro
            </v-btn>
<v-form ref="formularioreservas" v-model="valid" lazy-validation> 
 
 <v-text-field
            v-model="reserva.id"
            :rules="regla.obligatorio"
            label="Id"
            required
          ></v-text-field>
          <v-text-field
            v-model="reserva.usuario"
            :rules="regla.obligatorio"
            label="usuario"
            required
          ></v-text-field>
 <v-text-field
            v-model="reserva.instalacion"
            :rules="regla.obligatorio"
            label="instalacion"
            required
          ></v-text-field>
  <v-text-field
            v-model="reserva.fecha"
            :rules="regla.obligatorio"
            label="fecha"
            required
          ></v-text-field>     
  <v-text-field
            v-model="reserva.personasn"
            :rules="regla.obligatorio"
            label="Numero de personas"
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
            editar reserva
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
      let id_reserva=params.id;
      return {id_reserva}
    },
   data: () => ({
      valid: true,
      reserva:{},
      regla:{
          obligatorio:[ v => !!v || ' Is required'],
          email:[v => /.+@.+\..+/.test(v) || 'E-mail  be valid'],
      },
     
   }),
    beforeMount(){
      this.getreserva();
    },
   methods: {
      async getreserva()
      {
          try {
               let response= await this.$axios.get('http://localhost:3001/reservas/' + this.id_reserva );
            console.log(response);
            this.reserva=response.data
          } catch (error) {
             this.$swal(" error");
          }
        
      },
    
      async editar () {
        if (this.$refs.formularioreservas.validate()) {
              let reserva=Object.assign({},this.reserva);
            let response= await this.$axios.put('http://localhost:3001/reservas/' + this.id_reserva,reserva);
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
