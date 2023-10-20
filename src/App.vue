<script setup>
import { ref, reactive, watch, onMounted } from 'vue';
import { uid } from 'uid';

import Header from './components/Header.vue';
import Form from './components/Form.vue';
import Patient from './components/Patient.vue';

const patients = ref([]);

const patient = reactive({
  id: null,
  name: '',
  owner: '',
  email: '',
  date: '',
  symptom: '',
})

watch(
  patients,
  () => {
    savePatientsLocalStorage();
  },
  { deep: true }
);

onMounted(() => {
  if (localStorage.getItem('patients')) {
    patients.value = JSON.parse(localStorage.getItem('patients'));
  }
});

const savePatient = () => {
  if (patient.id) {
    const { id } = patient;

    const index = patients.value.findIndex(patient => patient.id === id);
    patients.value[index] = { ...patient };
  } else {
    patients.value.push({
      ...patient,
      id: uid(),
    });
  }

  // Reset form
  // patient.name = '';
  // patient.owner = '';
  // patient.email = '';
  // patient.date = '';
  // patient.symptom = '';

  // Otra forma de resetear el form
  Object.assign(patient, {
    name: '',
    owner: '',
    email: '',
    date: '',
    symptom: '',
    id: null
  })
}

// Actualizar el paciente
const updatePatient = (id) => {
  const patientEdit = patients.value.filter(patient => patient.id === id)[0];
  Object.assign(patient, patientEdit);


}

// Eliminar paciente
const deletePatient = (id) => {
  patients.value = patients.value.filter(patient => patient.id !== id);
}

// Almacenar pacientes en localStorage
const savePatientsLocalStorage = () => {
  localStorage.setItem('patients', JSON.stringify(patients.value));
}

</script>

<template>
  <div class="container max-w-5xl mx-auto mt-10">
    <Header />
    <div class="mt-10 md:flex">
      <Form v-model:name="patient.name" v-model:owner="patient.owner" v-model:email="patient.email"
        v-model:date="patient.date" v-model:symptom="patient.symptom" @save-patient="savePatient" :id="patient.id" />

      <div class="overflow-y-scroll md:w-1/2 md:h-screen">
        <h2 class="text-2xl font-black text-center">Administra tus pacientes</h2>
        <p class="my-5 text-lg text-center">Información de <span class="font-bold text-blue-600 ">pacientes</span>
        </p>
        <div v-if="patients.length" class="mt-10">
          <Patient v-for="patient in patients" :key="patient.id" :patient="patient" @update-patient="updatePatient"
            @delete-patient="deletePatient" />
        </div>
        <p v-else class="mt-10 text-lg text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>

