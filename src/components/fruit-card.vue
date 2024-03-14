<script setup></script>

<template>
  <div class="card-container">
    <div class="card">
      <div class="front">
        <img src="/image/guava.png" alt="guava" class="fruit-card" />
      </div>

      <div class="back"></div>
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
}
.front {
  background-color: rgb(19, 0, 144);
}
.fruit-card {
  height: 265px;
  width: 200px;
}
.back {
  background-color: pink;
  transform: rotateY(180deg);
}
.card:hover .front {
  transform: rotateY(180deg);
}
.card:hover .back {
  transform: rotateY(0deg);
}
</style>
