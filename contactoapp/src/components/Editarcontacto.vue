<template>
    <v-container>
        <v-layout>
            <v-flex>
                <h1>Editar datos de contacto</h1>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-card>
                <v-img :src="contactoeditar.avatar" alt="muestra_contacto">

                </v-img>
                <v-card-title>
                   <h1>Datos de contacto</h1>   
                </v-card-title>
                <v-card-text>
                   <v-layout>
                       <v-flex>
                           <v-text-field label="nombre" hide-details="auto" v-model="contactoeditar.first_name"></v-text-field>
                       </v-flex>
                   </v-layout>
                   <v-layout>
                       <v-flex>
                           <v-text-field label="apellido" hide-details="auto" v-model="contactoeditar.last_name" :disabled="true"></v-text-field>
                       </v-flex>
                   </v-layout>
                   <v-layout>
                       <v-flex>
                           <v-text-field label="Email" hide-details="auto" v-model="contactoeditar.email" :disabled="true"></v-text-field>
                       </v-flex>
                   </v-layout>
                </v-card-text>
                <v-divider></v-divider>
                <v-card-actions>
                    <v-btn color="error" @click="cancelar()">Cancelar</v-btn>
                    <v-btn color="success" @click="guarda()">Guardar</v-btn>
                </v-card-actions>

            </v-card>
        </v-layout>

    </v-container>
</template>
<script>
const axios = require('axios').default;
export default {
    name: 'Editarcontacto',
    props: {
        contacto: {}
    },
    data: function(){
        return{
            contactoeditar: {}
        }
    },
    components: {
    },
    mounted: function() {
        let self = this;
        self.contactoeditar = this.contacto;

    },
    methods: {
        guarda(){
            let self = this;
            // console.log(self.contactoeditar);
            axios.post('https://reqres.in/api/users', {
                name: self.contactoeditar.first_name,
                job: 'Flintstone'
            }).then(function (response) {
                // console.log(response);

                self.contactoeditar = response.data.name;
                self.last_name = response.data.job;
                self.$root.$emit('cerraredicion',false);


            }).catch(function (error) {
                console.log(error);
            });
        },
        cancelar(){
            let self = this;
            self.$root.$emit('cerraredicion',false);
        }
    }
}
</script>