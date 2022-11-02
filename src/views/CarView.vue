<template>
  <div class="container">
    <div v-if="car">
      <h1>The Car</h1>
      <h2>Make: {{ car.make }}</h2>
      <h3>Body: {{ car.body }}</h3>
      <h4>Year :{{ car.year }}</h4>
    </div>
    <div v-else>
      <h2>Car not Found</h2>
    </div>
  </div>
</template>

<script setup>
import { onBeforeMount, ref } from 'vue';
import { useRoute } from 'vue-router';
import CarData from '../data.json';

const {
  params: { id },
} = useRoute();

const car = ref(null);
onBeforeMount(() => {
  car.value = CarData.find((car) => car.id === parseInt(id));
});
</script>

<style></style>
