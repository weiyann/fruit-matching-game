<script setup>
import card from '@/components/fruit-card.vue'
import { ref } from 'vue'
import data from '../data/fruit-data.json'

const fruitData = ref(data)
const rotateFruit = (clickedFruit) => {
  console.log(clickedFruit)
  if (clickedFruit.side === 'back') {
    clickedFruit.side = 'front'
  }
}
</script>

<template>
  <main>
    <div v-for="fruit in fruitData" :key="fruit.id">
      <card :fruit="fruit" @rotateFruit="rotateFruit" />
    </div>
  </main>
</template>

<style scoped>
main {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 50px;
}
</style>
