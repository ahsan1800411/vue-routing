<script setup>
import { onMounted, ref, watch } from 'vue';
import carsData from '../data.json';
import { useRouter, useRoute } from 'vue-router';

const cars = ref(carsData);
const make = ref('');
const { query } = useRoute();

watch(make, () => {
  if (make.value && make.value === 'All') {
    cars.value = carsData;
  } else {
    cars.value = carsData.filter((car) => car.make === make.value);
  }
});

const { push } = useRouter();

const handleChange = () => {
  push({ query: { make: make.value } });
};

onMounted(() => {
  make.value = query.make || '';
});
</script>

<template>
  <main class="container">
    <h1>Our Cars</h1>
    <select v-model="make" @change="handleChange">
      <option value="All">All</option>
      <option value="Chevrolet">Chevrolet</option>
      <option value="Porsche">Porsche</option>
      <option value="Audi">Audi</option>
    </select>
    <div class="cards">
      <div
        class="card"
        v-for="car in cars"
        :key="car.id"
        @click="push(`/car/${car.id}`)"
      >
        <h2>{{ car.make }}</h2>
        <h4>{{ car.price }}$</h4>
      </div>
    </div>
  </main>
</template>

<style scoped>
.cards {
  display: flex;
  width: 1000px;
  flex-wrap: wrap;
  margin-top: 50px;
  justify-content: center;
}
.card {
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.207);
  padding: 15px;
  width: 150px;
  margin-right: 15px;
  cursor: pointer;
  margin-bottom: 20px;
}
</style>
