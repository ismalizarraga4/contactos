<template>
    <v-container>
        <v-layout>
            <v-flex>
                <h1>Detalle Contacto</h1>
            </v-flex>
            <v-flex>
                <Detalle/>
            </v-flex>
        </v-layout>
    </v-container>
</template>
<script>
import Detalle from '@/components/Detalle.vue'
export default {
    name: 'Contactodetalle',
    components: {
        Detalle
    }
}
</script>