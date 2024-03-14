<script setup>
const { fruit } = defineProps(['fruit'])
console.log(fruit)
</script>

<template>
  <div class="card-container">
    <div class="card" @click="$emit('rotateFruit', fruit)">
      <div :class="{ front: true, 'front-rotate': fruit.side === 'front' }">
        <img :src="fruit.src" :alt="fruit.name" class="fruit-card" />
      </div>

      <div :class="{ back: true, 'back-rotate': fruit.side === 'front' }"></div>
    </div>
  </div>
</template>

<style scoped>
.card {
  height: 285px;
  width: 220px;
  position: relative;
  transform-style: preserve-3d;
  perspective: 1000px;
  cursor: pointer;
}
.front,
.back {
  height: 285px;
  width: 220px;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  backface-visibility: hidden;
  transition: all 0.5s;
  border-radius: 10px;
}
.front {
  background-color: rgb(19, 0, 144);
  transform: rotateY(180deg);
}
.fruit-card {
  height: 265px;
  width: 200px;
}
.back {
  background-color: pink;
}
.front-rotate {
  transform: rotateY(0deg);
}
.back-rotate {
  transform: rotateY(180deg);
}

/* .card:hover .front {
  transform: rotateY(0deg);
}
.card:hover .back {
  transform: rotateY(180deg);
} */
</style>
