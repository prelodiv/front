<template>

   <v-row justify="center" align="center">
        <v-col cols="12">
            <v-card flat>
              <h1 style="text-align:center;">lista de reservas</h1>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn rounded color="rgb(30, 181,181, 0.9)" class="text-none; " to="/reservas/reserva">agregar reserva</v-btn>
              </v-card-actions>
        
              <v-data-table
                :headers="headers"
                :items="reserva"
                :items-per-page="5"
                class="elevation-1"
                >
                <template v-slot:item.actions="{ item }">
      <v-icon
        small
        class="mr-2"
        @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        small
        @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>

    </template>
             </v-data-table>
            </v-card>

        </v-col>
    </v-row>  



    
</template>

<script>
  export default {
    
    layout:"lHome",
      beforeMount(){
          this.getreserva();
      },
    data () {
      return {
        headers: [
          {
            text: 'id',
            align: 'start',
            value: 'id',
          },
          { text: 'usurario', value: 'usuario'},
          { text: 'instalacion', value: 'instalacion'},
          { text: 'fecha', value: 'fecha'},
          { text: 'numero de personas', value: 'personasn'},


          { text: 'Acción', value: 'actions' }
        ],
        reserva: [],
      };
    },
        methods:{
             async getreserva()
      {
          try {
            let response= await this.$axios.get('http://localhost:3001/reservas')
            this.reserva=response.data ;
          } catch (error) {
              
          }
        
      },
      
      editItem(item)
      {
        let url= "reservas/" + item.id;
        this.$router.push(url)
      },
      deleteItem(item)
  {
   this.$swal.fire({
  type:"warning",
  title: 'seguro?',
  text: "vas a borrar una reserva!",
  icon: 'warning',
  allowEscapeKey:false,
  allowOutsideClick:false,
  showCancelButton:true,
}).then(async(result) => {
  if (result.value) {
    try{
      let url='http://localhost:3001/reservas/' + item.id ;
      let response= await this.$axios.delete(url);
      this.$swal.fire({
        type:"success",
        title:"operacion exitosa.",
        text:"la reserva se elimino correctamente"
      });
      this.getreserva();
    
    }catch (error){
      this.$swal.fire({
        type:"error",
        title:"ha ocurrido un problema al eliminar",
        text: error.toString(),
      });
      }
      }
    
    }
  );

      },

        }
  }
</script>