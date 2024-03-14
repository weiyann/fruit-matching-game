<script setup>
import card from '@/components/fruit-card.vue'
import { ref } from 'vue'
import data from '../data/fruit-data.json'

const fruitData = ref(data)
const openCard = ref([])

const rotateFruit = (clickedFruit) => {
  if (clickedFruit.side === 'back') {
    clickedFruit.side = 'front'
    openCard.value.push(clickedFruit.name) // 將點擊的卡片的名稱添加到已翻開卡片數組中
    if (openCard.value.length === 2) {
      // 如果已翻開卡片數組中有兩個名稱
      compareCards() // 比較兩張卡片
    }
  } else {
    // 如果已翻開的卡片再次被點擊，則將其翻回
    clickedFruit.side = 'back'
    openCard.value.pop()
  }
}

const compareCards = () => {
  if (openCard.value[0] === openCard.value[1]) {
    // 如果兩張卡片的名稱相同
    openCard.value = [] // 清空已翻開卡片數組
  } else {
    setTimeout(() => {
      fruitData.value.forEach((fruit) => {
        if (fruit.name === openCard.value[0] || fruit.name === openCard.value[1]) {
          fruit.side = 'back'
        }
      })
      openCard.value = []
    }, 1000)
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
