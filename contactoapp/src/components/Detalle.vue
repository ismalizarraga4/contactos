<template>
    <v-container>
        <v-layout>
            <v-flex>
                <h1>Detalle de contacto numero: {{ $route.params.idcontacto }}</h1>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-card>
                <v-img :src="usuario.avatar" alt="muestra_contacto">

                </v-img>
                <v-card-title>
                   <h1>Detalle de contacto</h1>   
                </v-card-title>
                <v-card-text>
                   <h1 class="nombre_usuario">{{usuario.first_name}} {{usuario.last_name}}</h1>
                    <h1 class="email_usuario">{{usuario.email}}</h1>
                </v-card-text>
                <v-divider></v-divider>
                <v-card-actions>
                   <v-btn @click="muestraeditar = true">Editar</v-btn>
                </v-card-actions>

            </v-card>
        </v-layout>

        <!-- inicio modal/dialog -->
        <v-dialog v-model="muestraeditar" width="500" persistent>
            <v-card>
               <Editarcontacto :contacto="usuario"/>
            </v-card>
        </v-dialog>
       <!-- final modal/dialog -->

    </v-container>
</template>
<script>
const axios = require('axios').default;
import Editarcontacto from '@/components/Editarcontacto.vue' 
export default {
    name:'Detalle',
    data: function(){
        return {
            usuario: {},
            muestraeditar: false
        }
    },
    created(){
        let self = this;
        this.$root.$on("cerraredicion", function(val){
            self.muestraeditar = val;
        });
    },
    mounted: function(){
        let self = this;
        axios.get('https://reqres.in/api/users/'+ self.$route.params.idcontacto).then(data => {
            self.usuario = data.data.data;
        }).catch(e => console.log(e));
    },
    beforeCreate: function(){
        let self = this;
        axios.get('https://reqres.in/api/users/'+ self.$route.params.idcontacto).then(data => {
            self.usuario = data.data.data;
        }).catch(e => console.log(e));
    },
    methods: {
        editar: function(){
            let self = this;
            self.muestraeditar = true;
        }
    },
    components: {
        Editarcontacto
    }
}
</script>