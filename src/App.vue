<script setup>
import { ref, computed } from "vue";
const name = `vue dinamico`;

const counter = ref(0);

const arrayFavoritos = ref([0]);

const incremento = () => counter.value++;

const decremento = () => counter.value--;

const reset = () => (counter.value = 0);

const add = () => {
  arrayFavoritos.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
  console.log(numSearch);
  if (numSearch === 0) return true;
  return numSearch ? true : false;
});

const classCounter = computed(() => {
  if (counter.value === 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  }
  if (counter.value < 0) {
    return "negative";
  }
});
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
    <button @click="incremento" class="btn btn-success">aumentar</button>
    <button @click="decremento" class="btn btn-danger">disminuir</button>
    <button @click="reset" class="btn btn-secondary">reset</button>
    <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">
      add
    </button>
  </div>
    <ul class="list-group">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index">
        {{ num }}
      </li>
    </ul>
  </div>
</template>
<style>
h1 {
  color: blue;
}
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: black;
}
</style>
