<template>
    <div>
        <h1>usuarios</h1>
        <div>
            <h1>{{mensaje}}</h1>
            <h1>{{otra}}</h1>
        </div>
        <div class="cuenta_usuarios">
            <h1>{{ cuentaUsuarios}}</h1>
        </div>
        <div class="usuario" v-for="item of datosUsuario" :key="item.id">
            <div class="avatar_usuairo">
                <img alt="Vue logo" :src="item.avatar">
            </div>
            <div class="datos_usuario">
                <h1 class="nombre_usuario">{{item.first_name}} {{item.last_name}}</h1>
                <h1 class="email_usuario">{{item.email}}</h1>
            </div>
        </div>
    </div>
</template>
<script>
const axios = require('axios').default;
module.exports = {
    name: 'users',
    data: function(){
        return{
            mensaje: 'hola usuarios',
            otra: 'esto es otro mensaje',
            datosUsuario: []
        }
    },
    mounted: function(){
        let self = this;

        axios.get('https://reqres.in/api/users?page=2').then(data => {
            self.datosUsuario = data.data.data;
        }).catch(e => console.log(e));

    },
    computed: {
        cuentaUsuarios: function(){
            let self = this;
            return self.datosUsuario.length;
        }
    }
}

</script>
<style>

</style>