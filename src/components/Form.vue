<script setup>
import { reactive, computed } from 'vue';
import Alert from './Alert.vue';

const props = defineProps({
  id: {
    type: [String, null],
    required: true
  },
  name: {
    type: String,
    required: true
  },
  owner: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  date: {
    type: String,
    required: true
  },
  symptom: {
    type: String,
    required: true
  },
})

const emit = defineEmits(['update:name', 'update:owner', 'update:email', 'update:date', 'update:symptom', 'save-patient']);

const alert = reactive({
  message: '',
  type: '',
})

const isEditing = computed(() => props.id);

const validateFields = () => {
  // Validar form
  if (Object.values(props).includes('')) {
    alert.message = 'Todos los campos son obligatorios';
    alert.type = 'error';
    return;
  }

  emit('save-patient');

  // Mostrar alerta de éxito
  alert.message = 'Paciente agregado correctamente';
  alert.type = 'success';

  setTimeout(() => {
    Object.assign(alert, {
      message: '',
      type: ''
    })
  }, 3000);
}

</script>

<template>
  <div class="md:w-1/2">
    <h2 class="text-2xl font-black text-center">Seguimiento de Pacientes</h2>
    <p class="my-5 text-lg text-center">Añade pacientes y <span class="font-bold text-blue-600 ">administralos</span> </p>

    <Alert :alert="alert" v-if="alert.message" />

    <!-- Events modifiers -->
    <form @submit.prevent="validateFields" class="px-8 pt-6 pb-8 mt-10 mb-4 bg-white rounded shadow-md">

      <div class="mb-5">
        <label for="name" class="block mb-2 text-sm font-bold text-gray-700">Nombre de tu mascota</label>
        <!-- :value="name" @input="name = $event.target.value" -->
        <input type="text" name="name" id="name" placeholder="Nombre de tu mascota" :value="name"
          @input="$emit('update:name', $event.target.value)"
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded shadow appearance-none focus:outline-none focus:shadow-outline" />
      </div>

      <div class="mb-5">
        <label for="owner" class="block mb-2 text-sm font-bold text-gray-700">Nombre del propietario</label>
        <input type="text" name="owner" id="owner" placeholder="Nombre del propietario" :value="owner"
          @input="$emit('update:owner', $event.target.value)"
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded shadow appearance-none focus:outline-none focus:shadow-outline" />
      </div>

      <div class="mb-5">
        <label for="email" class="block mb-2 text-sm font-bold text-gray-700">Email</label>
        <input type="email" name="email" id="email" placeholder="Email del propietario" :value="email"
          @input="$emit('update:email', $event.target.value)"
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded shadow appearance-none focus:outline-none focus:shadow-outline" />
      </div>

      <div class="mb-5">
        <label for="date" class="block mb-2 text-sm font-bold text-gray-700">Fecha de alta</label>
        <input type="date" name="date" id="date" :value="date" @input="$emit('update:date', $event.target.value)"
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded shadow appearance-none focus:outline-none focus:shadow-outline" />
      </div>

      <div class="mb-5">
        <label for="date" class="block mb-2 text-sm font-bold text-gray-700">Síntomas</label>
        <textarea name="symptoms" id="symptoms" cols="30" rows="10" placeholder="Describe los síntomas de tu mascota"
          :value="symptom" @input="$emit('update:symptom', $event.target.value)"
          class="w-full px-3 py-2 leading-tight text-gray-700 rounded shadow appearance-none focus:outline-none focus:shadow-outline"></textarea>
      </div>

      <button type="submit"
        class="w-full px-3 py-2 font-bold text-white bg-blue-600 rounded shadow cursor-pointer hover:bg-blue-700 focus:shadow-outline">
        {{ isEditing ? 'Actualizar paciente' : 'Agregar paciente' }}
      </button>
    </form>
  </div>
</template>

<style lang="scss" scoped></style>