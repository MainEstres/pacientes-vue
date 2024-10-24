<script setup>
const props = defineProps({
    nombre: String,
    fecha: String,
    hora: String,
    gravedad: String,
    motivo: String
})

const color = (gravedad)=> {
    if(gravedad === 'Grave'){
        return 'red'
    }if (gravedad === 'Leve') {
        return 'yellow'
    } else {
        return 'green'
    }
}

</script>

<template>

    <div class="card text-center ms-3"  style="width: 18rem;" :style="{backgroundColor: color(gravedad)}">
        <h3>Paciente: {{ nombre }}</h3>
        <h4>Fecha: {{ fecha }}</h4>
        <h4>Hora: {{ hora }}</h4>
        <h4>Gravedad: {{ gravedad }}</h4>
        <h4>Motivo: {{ motivo }}</h4>
        <button @click="$emit('eliminarPaciente')">Eliminar</button>
    </div>

</template>

<style scoped></style>