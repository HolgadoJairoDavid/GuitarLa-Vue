<script setup>
import {ref, reactive, onMounted} from 'vue'
import {db} from './data/guitarras'
import Guitarra from './components/Guitarra.vue'

const guitarras = ref([])

onMounted(() => {
    guitarras.value = db
})
const agregarCarrito = () => {
    alert('Diste click')
}
</script>


<template>
   <header class="py-5 header">
        <div class="container-xl">
            <div class="row justify-content-center justify-content-md-between">
                <div class="col-8 col-md-3">
                    <a href="index.html">
                        <img class="img-fluid" src="/img/logo.svg" alt="imagen logo">
                    </a>
                </div>
                <nav class="col-md-6 a mt-5 d-flex align-items-start justify-content-end">
                    <div 
                        class="carrito"
                    >
                        <img class="img-fluid" src="/img/carrito.png" alt="imagen carrito" />

                        <div id="carrito" class="bg-white p-3">
                            <p class="text-center">El carrito esta vacio</p>
                            <table class="w-100 table">
                                <thead>
                                    <tr>
                                        <th>Imagen</th>
                                        <th>Nombre</th>
                                        <th>Precio</th>
                                        <th>Cantidad</th>
                                        <th></th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>
                                            <img class="img-fluid" src="/img/guitarra_02.jpg" alt="imagen guitarra">
                                        </td>
                                        <td>SRV</td>
                                        <td class="fw-bold">
                                                $299
                                        </td>
                                        <td class="flex align-items-start gap-4">
                                            <button
                                                type="button"
                                                class="btn btn-dark"
                                            >
                                                -
                                            </button>
                                                1
                                            <button
                                                type="button"
                                                class="btn btn-dark"
                                            >
                                                +
                                            </button>
                                        </td>
                                        <td>
                                            <button
                                                class="btn btn-danger"
                                                type="button"
                                            >
                                                X
                                            </button>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>

                            <p class="text-end">Total pagar: <span class="fw-bold">$899</span></p>
                            <button class="btn btn-dark w-100 mt-3 p-2">Vaciar Carrito</button>
                        </div>
                    </div>
                </nav>
            </div><!--.row-->

            <div class="row mt-5">
                <div class="col-md-6 text-center text-md-start pt-5">
                    <h1 class="display-2 fw-bold">Modelo VAI</h1>
                    <p class="mt-5 fs-5 text-white">Lorem ipsum dolor sit amet consectetur adipisicing elit. Temporibus, possimus quibusdam dolor nemo velit quo, fuga omnis, iure molestias optio tempore sint at ipsa dolorum odio exercitationem eos inventore odit.</p>
                    <p class="text-primary fs-1 fw-black">$399</p>
                    <button 
                        type="button"
                        class="btn fs-4 bg-primary text-white py-2 px-5"
                    >Agregar al Carrito</button>
                </div>
            </div>
        </div>

        <img class="header-guitarra" src="/img/header_guitarra.png" alt="imagen header">
    </header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitarra v-for="guitarra in guitarras" :guitarra="guitarra" @agregar-carrito="agregarCarrito"/>
        </div>
    </main>


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>
</template>


