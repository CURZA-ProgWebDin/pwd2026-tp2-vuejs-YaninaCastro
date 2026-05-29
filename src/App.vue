<template>
  <div>
    <h1>Gestión de Productos</h1>

    <!-- form -->
    <ProductoForm @agregar-producto="agregarProducto" />

    <!-- filtro -->
    <select v-model="filtroCategoria">
      <option value="">Todas</option>
      <option value="Tecnología">Tecnología</option>
      <option value="Ropa">Ropa</option>
      <option value="Hogar">Hogar</option>
    </select>

    <p>Total productos: {{ totalProductos }}</p>
    <p>Valor inventario: ${{ valorInventario }}</p>

    <!-- LISTA -->
    <ProductoLista
      :productos="productosFiltrados"
      @eliminar="eliminarProducto"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

import ProductoForm from './components/ProductoForm.vue'
import ProductoLista from './components/ProductoLista.vue'


const productos = ref([])
const filtroCategoria = ref('')


const agregarProducto = (producto) => {
  const nuevoProducto = {
    id: Date.now(),
    ...producto
  }

  productos.value.push(nuevoProducto)
}

const eliminarProducto = (id) => {
  productos.value = productos.value.filter(
    producto => producto.id !== id
  )
}


const productosFiltrados = computed(() => {
  if (filtroCategoria.value === '') {
    return productos.value
  }

  return productos.value.filter(
    p => p.categoria === filtroCategoria.value
  )
})


const totalProductos = computed(() => {
  return productos.value.length
})


const valorInventario = computed(() => {
  return productos.value.reduce((total, producto) => {
    return total + (producto.precio * producto.stock)
  }, 0)
})
</script>
