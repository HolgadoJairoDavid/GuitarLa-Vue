<script setup>
import { ref, reactive, onMounted, watch } from "vue";
import { db } from "./data/guitarras";
import Guitarra from "./components/Guitarra.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

const guitarras = ref([]);
const carrito = ref([]);
const guitarra = ref({})

const guardarLocalStorage = () => {
    localStorage.setItem('carrito', JSON.stringify(carrito.value))
}
watch(carrito, () => {
guardarLocalStorage()
}, {
    deep: true
})
onMounted(() => {
  guitarras.value = db;
  guitarra.value = db[3]

  const carritoStorage = localStorage.getItem('carrito')
  if(carritoStorage){
    carrito.value = JSON.parse(carritoStorage)
  }
});

const agregarCarrito = (guitarra) => {
  const existeGuitarra = carrito.value.findIndex(
    (producto) => producto.id === guitarra.id
  );
  if (existeGuitarra >= 0) {
    carrito.value[existeGuitarra].cantidad++;
  } else {
    guitarra.cantidad = 1;
    carrito.value.push(guitarra);
  }
};

const decrementarCantidad = (id) => {
  const index = carrito.value.findIndex((producto) => producto.id === id);
  if(carrito.value[index].cantidad<= 1) return
  carrito.value[index].cantidad--;
};

const aumentarCantidad = (id) => {
  const index = carrito.value.findIndex((producto) => producto.id === id);
  if(carrito.value[index].cantidad >= 5) return
  carrito.value[index].cantidad++;
};

const eliminarProducto = (id) => {
carrito.value = carrito.value.filter(producto => producto.id !== id)
}
const vaciarCarrito = () => {
    carrito.value = []
}
</script>

<template>
  <Header
    :carrito="carrito"
    :guitarra="guitarra"
    @eliminar-producto="eliminarProducto"
    @aumentar-cantidad="aumentarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @vaciar-carrito = "vaciarCarrito"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <Guitarra
        v-for="guitarra in guitarras"
        :key="guitarra.id"
        :guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </main>

  <Footer></Footer>
</template>
