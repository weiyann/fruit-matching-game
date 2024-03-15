<script setup>
import card from '@/components/fruit-card.vue'
import { ref } from 'vue'
import data from '../data/fruit-data.json'

//亂數排序
const randomData = data.sort(() => 0.5 - Math.random())
const fruitData = ref(randomData)
const openCard = ref([])

// 遊戲通關的變數
let gameCompleted = ref(false)

// 翻轉卡片的函式
const rotateFruit = (clickedFruit) => {
  if (clickedFruit.side === 'back') {
    clickedFruit.side = 'front'
    openCard.value.push(clickedFruit.name) // 將點擊的卡片的名稱添加到陣列
    if (openCard.value.length === 2) {
      // 如果陣列裡有兩個值
      compareCards()
    }
  }
}
// 比較卡片名字的函式
const compareCards = () => {
  if (openCard.value[0] === openCard.value[1]) {
    // 如果兩張卡片的名稱相同
    openCard.value = [] // 清空陣列
    checkGameCompletion() // 呼叫確認是否通關
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

// 確認是否通關的函式
const checkGameCompletion = () => {
  const matchedCards = fruitData.value.filter((fruit) => fruit.side === 'front')
  if (matchedCards.length === fruitData.value.length) {
    gameCompleted.value = true
  }
}
</script>

<template>
  <header>
    <h1>Fruit Matching Game</h1>
    <p>Find matching fruit pairs!</p>
    <p v-if="gameCompleted">Congratulations! You completed the game!</p>
  </header>
  <main>
    <div v-for="fruit in fruitData" :key="fruit.id">
      <card :fruit="fruit" @rotateFruit="rotateFruit" />
    </div>
  </main>
</template>

<style scoped>
header {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding-bottom: 20px;
}
main {
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(4, 1fr);
  gap: 50px;
}
</style>
