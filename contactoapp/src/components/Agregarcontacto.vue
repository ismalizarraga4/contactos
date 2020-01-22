<template>
    <v-container>
        <v-layout>
            <v-flex>
                <h1>Ingresar datos del contacto</h1>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-flex>
                <v-file-input type="file" name="image" @change="getImage" accept="image/*" label="avatar"></v-file-input>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-flex>
                <v-text-field label="nombre" :rules="rules" hide-details="auto" v-model="contactoagregar.first_name"></v-text-field>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-flex>
                <v-text-field label="apellido" :rules="rules" hide-details="auto" v-model="contactoagregar.last_name"></v-text-field>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-flex>
                <v-text-field label="Email" :rules="rules" hide-details="auto" v-model="contactoagregar.email"></v-text-field>
            </v-flex>
        </v-layout>
        <v-divider></v-divider>
        <v-card-actions>
            <v-btn color="error" @click="cerrar()">Cancelar</v-btn>
            <v-btn color="success" @click="guarda()">Guardar</v-btn>
        </v-card-actions>
    </v-container>
</template>

<script>
const axios = require('axios').default;
export default {
    name: 'Agregarcontacto',
    props: {
        contacto: {}
    },
    data: function(){
        return{
            contactoagregar: {
                first_name: '',
                last_name: '',
                email: '',
                avatar: ''
            }
        }
    },
    methods : {
            getImage(event){
                let self = this;
                //Asignamos la imagen a  nuestra data
                self.contactoagregar.avatar = event.target.files[0];
            },

            guarda(){
                let self = this;
                axios.post('https://reqres.in/api/users', {
                    name: self.contactoagregar.first_name,
                    job:  self.contactoagregar.last_name
                }).then(function (response) {
                    
                    self.contactoagregar.first_name = response.data.name;
                    self.contactoagregar.last_namelast_name = response.data.job;
                    self.$root.$emit('cerraagregar',false);
                    console.log(response);
                }).catch(function (error) {
                    console.log(error);
                });

                self.contactoagregar = {
                    first_name: '',
                    last_name: '',
                    email: '',
                    avatar: ''
                }
            },
            cerrar(){
                debugger;
                let self = this;
                self.$root.$emit('cerraagregar',false);
            }

        }
}
</script>