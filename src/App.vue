<template>
  <h2>Cena {{ contador + 1 }} con el rey godo {{ rey }}</h2>
  <h3 class="precio"> Precio: {{ productos[contador].precio }} u$s</h3>
  <div v-if="productos[contador].finDeSemana" class="soloFinesDeSemana dias">(Sólo fines de Semana)</div>
  <div v-else class="todosLosDias dias">(De lunes a domingo)</div>
  <div v-if="productos[contador].precio < 100" class="oferta">
    <div class="precio">Ahora un 10% de descuento:{{ nuevoPrecio }} u$s</div>
    <img src="./assets/oferta.jpg" alt="rey godo en descuento" class="cartel">
  </div>
  <div class="rey"><img :src="imagen" alt="imagen del rey" style="margin-left: 100px">
    <button @:click="siguiente" style="margin: 10px 0 0 150px">Siguiente({{ contador + 1 }}/{{ total }})</button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { productos } from './datos.js'

const contador = ref(0)
const total = productos.length
const ruta = 'https://www.html6.es/img/rey_'

const siguiente = () => {
  contador.value++
  if (contador.value >= total) contador.value = 0
}

const rey = computed(() => {
  const elRey = productos[contador.value].nombre.toLowerCase()
  return elRey.substring(0, 1).toUpperCase() + elRey.substring(1)
})

const imagen = computed(() => {
  return `${ruta}${productos[contador.value].nombre.toLocaleLowerCase()}.png`
})

const nuevoPrecio = computed(() => {
  return Number(productos[contador.value].precio / 1.10).toFixed(2)
})
</script>

<style scoped>
h2 {
  display: flex;
  justify-content: center;
}

.todosLosDias {
  background-color: green;
  margin: 0px 157px
}

.soloFinesDeSemana {
  background-color: red;
  margin: 0px 157px
}

.dias {
  color: white;
  padding: 4px 17px;
  font-size: 0.9em;
  border-radius: 4px;
  display: flex;
  justify-content: center;
}

.oferta {
  width: 75px;
  margin: 10px 70px;
  display: grid;

}

.rey {
  width: 80%;
  padding: 5px;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;

}

.cartel {
  margin-left: 350px;
  padding: 2px;
  height: 40px;

}

.precio {
  display: flex;
  justify-content: center;
}
</style>
