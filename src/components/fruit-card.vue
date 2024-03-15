<script setup>
const { fruit } = defineProps(['fruit'])
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
  height: 100%;
  width: 100%;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  backface-visibility: hidden;
  transition: all 0.5s;
  border-radius: 10px;
}
.front {
  background-color: #1800b7;
  transform: rotateY(180deg);
}
.fruit-card {
  height: 90%;
  width: 90%;
}
.back {
  background-color: #1800b7;
  background-image: url('https://www.transparenttextures.com/patterns/diagonal-striped-brick.png');
}
.front-rotate {
  transform: rotateY(0deg);
}
.back-rotate {
  transform: rotateY(180deg);
}

@media screen and (max-width: 1200px) {
  .card {
    height: 200px;
    width: 150px;
  }
}

@media screen and (max-width: 760px) {
  .card {
    height: 150px;
    width: 100px;
  }
}
</style>
