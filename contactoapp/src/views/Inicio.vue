<template>
    <v-container>
        <v-layout>
            <v-flex>
                <h1>usuarios</h1>
                <h1>{{ cuentaUsuarios}}</h1>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-btn color="success" @click="muestraagregar = true">
                Agregar
            </v-btn>
        </v-layout>
        <v-layout>
            <v-simple-table>
                <thead>
                    <tr>
                    <th class="text-left">Numero Contacto</th>
                    <th class="text-left">Nombre</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="item of datosUsuario" :key="item.id">
                        <td>
                            <router-link :to="/Detallecontactos/+item.id">{{item.id}}</router-link>
                        </td>
                        <td>
                            <router-link :to="/Detallecontactos/+item.id">{{item.first_name}} {{item.last_name}}</router-link>
                        </td>
                    </tr>
                </tbody>
            </v-simple-table>
        </v-layout>

        <!-- inicio modal/dialog -->
        <v-dialog v-model="muestraagregar" width="500" persistent>
            <v-card>
               <agregarcontacto/>
            </v-card>
        </v-dialog>
       <!-- final modal/dialog -->
    </v-container>
</template>

<script>
import agregarcontacto from '@/components/Agregarcontacto.vue'
const axios = require('axios').default;
export default {
    name: 'Inicio',
    data: function(){
        return{
            datosUsuario: [],
            muestraagregar: false
        }
    },
    mounted: function(){
        let self = this;

        axios.get('https://reqres.in/api/users?page=2').then(data => {
            self.datosUsuario = data.data.data;
        }).catch(e => console.log(e));

        this.$root.$on("cerraagregar", function(val){
            debugger;
            self.muestraagregar = val;
        });

    },
    computed: {
        cuentaUsuarios: function(){
            let self = this;
            return self.datosUsuario.length;
        }
    },
    methods: {
      agregar: function(){
            let self = this;
            self.muestraagregar = true;
        }
    },
    components: {
        agregarcontacto
    }
}
</script>


<style>
.contacto{
  list-style: none;
}

</style>
