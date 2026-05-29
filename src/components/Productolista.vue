
<template>
  <ul>
    <ProductItem
      v-for="producto in productos"
      :key="producto.id"
      :producto="producto"
      @eliminar= "emit('eliminar', $event)"
    />
  </ul>
</template>


<script setup>
import ProductItem from './ProductItem.vue'

const props = defineProps({
  productos: Array
})

const emit = defineEmits(['eliminar'])
</script>
