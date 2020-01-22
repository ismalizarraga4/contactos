<template>
   <v-container>
       <v-layout>
           <v-flex class="primary" xs6>
               <h1>12</h1>
               <v-btn dark class="success" @click="dialogeditar = true">
                   muestra
               </v-btn>
           </v-flex>
       </v-layout>
       <v-simple-table>
            <template v-slot:default>
            <thead>
                <tr>
                <th class="text-left">Numero Contacto</th>
                <th class="text-left">Nombre</th>
                </tr>
            </thead>
            <tbody>
                
            </tbody>
            </template>
        </v-simple-table>

       <!-- inicio modal/dialog -->
       <v-dialog v-model="dialogeditar" width="500" persistent>
           <v-card>
               <v-card-title>este es el titulo</v-card-title>
               <v-card-text>
                   Lorem ipsum dolor sit, amet consectetur adipisicing elit. Iste error doloribus laudantium tempore delectus omnis consectetur eveniet? Hic id sapiente sed quae tempora at aut, labore cupiditate esse! Libero, deleniti.
               </v-card-text>
               <v-divider></v-divider>
               <v-card-actions>
                   <v-btn @click="dialogeditar = false">cerrar</v-btn>
               </v-card-actions>

           </v-card>
       </v-dialog>
       <!-- final modal/dialog -->
   </v-container>
</template>
<script>
const axios = require('axios').default;
export default {
  name: 'home',
  data: function(){
      return {
          dialogeditar: false,
          datosUsuario: []
      }
  },
  mounted: function(){
      debugger;
        let self = this;

        axios.get('https://reqres.in/api/users?page=2').then(data => {
            debugger;
            self.datosUsuario = data.data.data;
        }).catch(e => console.log(e));
    }
}
</script>