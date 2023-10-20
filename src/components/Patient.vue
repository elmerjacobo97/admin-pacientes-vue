<script setup>
const props = defineProps({
  patient: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['update-patient', 'delete-patient']);

</script>

<template>
  <div class="px-5 py-10 mx-5 my-10 bg-white shadow-md rounded-xl">
    <p class="mb-3 font-bold text-gray-700 uppercase">ID:
      <span class="font-normal normal-case">
        {{ patient.id }}
      </span>
    </p>

    <p class="mb-3 font-bold text-gray-700 uppercase">Nombre:
      <span class="font-normal normal-case">
        {{ patient.name }}
      </span>
    </p>

    <p class="mb-3 font-bold text-gray-700 uppercase">Propietario:
      <span class="font-normal normal-case">
        {{ patient.owner }}
      </span>
    </p>

    <p class="mb-3 font-bold text-gray-700 uppercase">Email:
      <span class="font-normal normal-case">
        {{ patient.email }}
      </span>
    </p>

    <p class="mb-3 font-bold text-gray-700 uppercase">Fecha Alta:
      <span class="font-normal normal-case">
        {{ patient.date }}
      </span>
    </p>

    <p class="mb-3 font-bold text-gray-700 uppercase">Síntomas:
      <span class="font-normal normal-case">
        {{ patient.symptom }}
      </span>
    </p>

    <div class="grid gap-5 mt-10 md:grid-cols-2 ">
      <button type="button"
        class="block w-full px-10 py-2 font-bold text-white uppercase bg-blue-600 rounded-lg hover:bg-indigo-700"
        @click="$emit('update-patient', patient.id)">Editar</button>

      <button type="button"
        class="block w-full px-10 py-2 font-bold text-white uppercase bg-red-600 rounded-lg hover:bg-red-700"
        @click="$emit('delete-patient', patient.id)">Eliminar</button>
    </div>
  </div>
</template>

