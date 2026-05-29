<template>
  <li>
    {{ producto.nombre }} -
    {{ producto.precio }} -
    {{ producto.stock }} -
    {{ producto.categoria }}

    <button @click="emit('eliminar', producto.id)">
      Eliminar
    </button>
  </li>
</template>


<script setup>
const props = defineProps({
  producto: Object
})

const emit = defineEmits(['eliminar'])
</script>

