<script setup>
import { ref } from 'vue';
import Tabla from './components/Tabla.vue';

const eliminar = (indice) => {
  pacientes.value.splice(indice, 1)
}

const agregarPaciente = () => {
  pacientes.value.push({ ...nuevoPaciente.value });
  nuevoPaciente.value = {
    nombre: "",
    fecha: "",
    hora: "",
    gravedad: "",
    motivo: ""
  };
}

const nuevoPaciente = ref({
  nombre: "",
  fecha: "",
  hora: "",
  gravedad: "",
  motivo: ""
})

const pacientes = ref([])

const colores = [
  {
    name: 'Grave'
  },
  {
    name: 'Leve'
  },
  {
    name: 'Normal'
  }
]


</script>

<template>

  <div class="container">
    <h1 class="text-center m-4">Ingresa tus datos</h1>

    <div class=" d-flex justify-content-center">
      
      <!--Form-->
      <form class="card" @submit.prevent="agregarPaciente">
        <div class="m-2">
          <label :class="{ labelError: !nuevoPaciente.nombre }">Paciente</label>
          <input v-model="nuevoPaciente.nombre" type="text">
        </div>

        <div class="m-2">
          <label :class="{ labelError: !nuevoPaciente.fecha }">Fecha</label>
          <input v-model="nuevoPaciente.fecha" type="date">
        </div>

        <div class="m-2">
          <label :class="{ labelError: !nuevoPaciente.hora }">Hora</label>
          <input v-model="nuevoPaciente.hora" type="time">
        </div>

        <div class="m-2">
          <label :class="{ labelError: !nuevoPaciente.gravedad }">Gravedad</label>
          <select v-model="nuevoPaciente.gravedad">
            <option v-for="color in colores" :value="color.name" :key="color.name">{{ color.name }}</option>
          </select>
        </div>

        <div class="m-2">
          <label :class="{ labelError: !nuevoPaciente.motivo }">Motivo</label>
          <input v-model="nuevoPaciente.motivo" type="text">
        </div>
        <button class="btn btn-primary">Agregar</button>
      </form>
    </div>


    <!--Texto Alert-->
    <div class="text-center" v-if="pacientes.length === 0" style="color: red;">
      <h2>No hay pacientes agregados</h2>
    </div>

    <!--Tabla con infoPaciente-->
    <div class="d-flex mt-4">
      <Tabla v-for="(paciente, i) in pacientes" :nombre="paciente.nombre" :fecha="paciente.fecha" :hora="paciente.hora"
        :gravedad="paciente.gravedad" :motivo="paciente.motivo" @eliminarPaciente="eliminar(i)">
      </Tabla>
    </div>

  </div>





</template>

<style scoped>
.labelError {
  color: red
}
</style>