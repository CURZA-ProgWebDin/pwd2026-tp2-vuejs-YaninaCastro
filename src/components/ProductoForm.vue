
<template>
  <form @submit.prevent="guardarProducto">
    <input type="text" placeholder="Nombre" v-model="nombre">

    <input type="number" placeholder="Precio" v-model="precio">

    <input type="number" placeholder="Stock" v-model="stock">

    <select v-model="filtroCategoria">
      <option value="">Todas</option>
      <option value="Tecnología">Tecnología</option>
      <option value="Ropa">Ropa</option>
      <option value="Hogar">Hogar</option>
    </select>

    <button type="submit">Guardar</button>
  </form>
  <p v-if="error">{{ error }}</p>

  <p>{{ nombre }}</p>
  <p>{{ precio }}</p>
  <p>{{ stock }}</p>
  <p>{{ categoria }}</p>

</template>


<script setup>
import { ref } from 'vue'

const emit = defineEmits(['agregar-producto'])

const nombre = ref('')
const precio = ref('')
const stock = ref('')
const categoria = ref('')
const error = ref('')

const guardarProducto = () => {
  console.log('Se ejecutó guardarProducto')
  if (
    nombre.value === "" ||
    precio.value === "" ||
    stock.value === "" ||
    categoria.value === "" 
  ){error.value= 'Todos los datos deben completarse'
  return
}


if (precio.value <= 0 || stock.value < 0) {
  error.value = 'Precio o stock inválidos' 
  return
}

error.value = ''

const producto = {
  nombre: nombre.value,
  precio: Number(precio.value),
  stock: Number(stock.value),
  categoria: categoria.value
}


emit('agregar-producto', producto)
}
</script>
