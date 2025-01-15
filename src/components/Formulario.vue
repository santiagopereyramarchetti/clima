<template>
    <form @submit.prevent="consultarClima" class="formulario" action="">
        <Alerta v-if="error">
            {{ error }}
        </Alerta>
        <div class="campo">
            <label for="ciudad">
                Ciudad
            </label>
            <input v-model="busqueda.ciudad" type="text" id="ciudad" placeholder="Ciudad">
        </div>
        <div class="campo">
            <label for="pais">
                Pais
            </label>
            <select v-model="busqueda.pais" id="pais">
                <option value="">-- Selecciona --</option>
                <option v-for="pais in paises" :value="pais.codigo">{{ pais.nombre }}</option>
            </select>
        </div>
        <input type="submit" value="Consultar clima">
    </form>
</template>

<script setup>
    import { ref, reactive } from "vue"

    import Alerta from "../components/Alerta.vue"

    const emits = defineEmits([
        'obtener-clima'
    ])

    const error = ref('')

    const paises = [
        { codigo: 'US', nombre: 'Estados Unidos' },
        { codigo: 'MX', nombre: 'México' },
        { codigo: 'AR', nombre: 'Argentina' },
        { codigo: 'CO', nombre: 'Colombia' },
        { codigo: 'CR', nombre: 'Costa Rica' },
        { codigo: 'ES', nombre: 'España' },
        { codigo: 'PE', nombre: 'Perú' }
    ]

    const busqueda = reactive({
        ciudad: '',
        pais: ''
    })

    const consultarClima = () => {
        if(Object.values(busqueda).includes('')){
            error.value = "Todos los campos son obligatorios"
        }else{
            error.value = ''
            emits('obtener-clima', busqueda)
        }
    }
    
</script>

<style scoped>

</style>