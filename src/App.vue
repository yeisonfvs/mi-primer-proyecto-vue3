<script setup>
import { ref, computed } from 'vue';

const name = 'Yeison';
const styleColor = 'color: pink';
const arrayColores = ['blue', 'red', 'green'];
const activo = true;
const arrayAnimales = [
  '🦓',
  '🫎',
  '🐩',
  '🦍',
  '🐨',
  '🐼',
];
const arrayArticulo = [
  {
    name: 'reloj',
    price: 33.3,
    description: 'marca rolrx',
    stock: 0,
  },
  {
    name: 'gorra',
    price: 2.2,
    description: 'marca totto',
    stock: 10,
  },
];
const objetoArt = {
  name: 'lapiz',
  price: 20,
  description: 'nuevo',
};
const handleClick = (mensaje) => {
  console.log(mensaje);
};
const counter = ref(0);
const increment = () => counter.value++;
const decrement = () => counter.value--;
const reset = () => (counter.value = 0);

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'zero';
  }
  if (counter.value > 0) {
    return 'positive';
  }
  if (counter.value < 0) {
    return 'negative';
  }
});
const arrayNum = ref([]);
const agregar = () => {
  arrayNum.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayNum.value.find((num) => num === counter.value);
  if (numSearch === 0) return true;
  return numSearch ? true : false;
});
</script>

<template>
  <div class="container text-center">
    <h1>Hola {{ name.toUpperCase() }} !</h1>
    <h2 :style="`color: ${arrayColores[1]}`">Soy Azul</h2>
    <h2>{{ arrayColores }}</h2>
    <h3>{{ activo ? 'estoy activo' : 'estoy inactivo' }}</h3>
    <h3 v-if="activo">estoy activo2</h3>
    <p v-else="!activo">estoy inactivo2</p>
    <p v-show="activo">v-show</p>
    <ul class="list-group">
      <li
        v-for="(animal, index) in arrayAnimales"
        :key="animal"
        class="fs-1 list-group-item"
      >
        {{ index }} {{ animal }}
      </li>
    </ul>

    <ul>
      <template v-for="(art, index) in arrayArticulo" :key="art.name">
        <li v-if="art.stock > 0">
          {{ index }} {{ art.name }} - {{ art.price }} - {{ art.description }} -
          {{ art.stock }}
        </li>
      </template>
    </ul>

    <ul>
      <li v-for="(value, propiedad, index) in objetoArt" :key="value">
        {{ index }} {{ propiedad }} : {{ value }}
      </li>
    </ul>

    <button
      class="btn btn-primary m-2"
      @click.right.prevent="handleClick('texto right')"
    >
      Activame right
    </button>
    <button class="btn btn-secondary m-2" @click="handleClick('texto left')">
      Activame left
    </button>
    <button
      class="btn btn-light m-2"
      @click.middle="handleClick('texto middle')"
    >
      Activame middle
    </button>
    <!-- <h2 :class="counter > 0 ? 'positive' : 'negative'">{{ counter }}</h2> -->

    <div class="container">
      <h2 class="text-center m-3" :class="classCounter">{{ counter }}</h2>
      <button class="btn btn-success m-2" @click="increment">Aumentar</button>
      <button class="btn btn-danger m-2" @click="decrement">Disminuir</button>
      <button class="btn btn-outline-light m-2" @click="reset">Resetear</button>
      <button
        class="btn btn-outline-primary m-2"
        @click="agregar"
        :disabled="bloquearBtnAdd"
      >
        Add
      </button>
      <h2 class="text-center" v-for="num in arrayNum">{{ num }}</h2>
    </div>
  </div>
</template>

<style>
h1 {
  color: #0ad159;
}
.positive {
  color: #0ad159;
}
.negative {
  color: red;
}
.zero {
  color: #f110e6;
}
</style>
