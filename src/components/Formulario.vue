<script setup>
import { reactive, computed } from 'vue'
import Alerta from './Alerta.vue'

const alerta = reactive({
    tipo:'',
    mensaje:''
}) 

const emit =   defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:email', 'update:alta', 'update:sintoma', 'guardar-paciente'])

const props = defineProps({
    id: {
        type: [String, null],
        required: true
    },
    nombre: {
        type: String,
        required: true
    },
    propietario: {
        type: String,
        required: true
    },
    email: {
        type: String,
        required: true
    },
    alta: {
        type: String,
        required: true
    },
    sintoma: {
        type: String,
        required: true
    },
})

const validar = e => {
    if(Object.values(props).includes('')){
       alerta.mensaje = 'Todos los campos son obligatorios'
       alerta.tipo = 'error'
       return
    }
    emit('guardar-paciente')
    alerta.mensaje = 'Paciente almacenado correctamente'
    alerta.tipo = 'exito'
    setTimeout(()=>{
        Object.assign(alerta, {
            tipo: '',
            mensaje: ''
        })
    }, 3000)
}

const editando = computed(()=>{ props.id
})

</script>

<template>
    <div class="md:w-1/2 px-[10px]">
        <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade pacientes y <span class="text-indigo-600 font-bold">Administralos</span>
        </p>
        <Alerta v-if="alerta.mensaje" :alerta="alerta"/>
        <form class="bg-white shadow-md rounded-lg py-10 px-5 mb-10" @submit.prevent="validar">
            <div class="mb-5">
                <label for="mascota" class="block text-gray-700 uppercase font-bold text-[12px]">
                    Nombre mascota
                </label>
                <input id="mascota" type="text" placeholder="Nombre de la mascota" :value="nombre" @input="$emit('update:nombre', $event.target.value)"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md placeholder:text-[12px]">
            </div>
            <div class="mb-5">
                <label for="propietario" class="block text-gray-700 uppercase font-bold  text-[12px]">
                    Nombre propietario
                </label>
                <input id="propietario" type="text" placeholder="Nombre del propietario" :value="propietario" @input="$emit('update:propietario', $event.target.value)"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md placeholder:text-[12px]">
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold text-[12px]">
                    Email del propietario
                </label>
                <input id="email" type="email" placeholder="Email del propietario" :value="email" @input="$emit('update:email', $event.target.value)"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md placeholder:text-[12px]">
            </div>
            <div class="mb-5">
                <label for="alta" class="block text-gray-700 uppercase font-bold text-[12px]">
                    Alta
                </label>
                <input id="alta" type="date" placeholder="Alta de la mascota" :value="alta" @input="$emit('update:alta', $event.target.value)"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md placeholder:text-[12px]">
            </div>
            <div class="mb-5">
                <label for="sintoma" class="block text-gray-700 uppercase font-bold text-[12px]">
                    Síntomas
                </label>
                <input id="sintoma" type="textarea" placeholder="Describe los síntomas" :value="sintoma" @input="$emit('update:sintoma', $event.target.value)"
                    class="border-2  h-[80px] w-full p-2 mt-2 placeholder-gray-400 rounded-md placeholder:text-[12px]">
            </div>
            <input type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase rounded-md font-bold text-[14px] hover:bg-indigo-700 cursor-pointer transition-colors"
                :value="[editando ? 'Guardar Cambios' : 'Registrar Paciente']">
        </form>
    </div>
</template>
