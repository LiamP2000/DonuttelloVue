<script setup>
import DonutCard from './components/DonutCard.vue'

</script>

<template>
  <div class="app">
    <h1>Donut Gallery</h1>
    <div class="donut-cards">
        <DonutCard />
        <DonutCard />
        <DonutCard />
      </div>
  </div>
  
  
</template>

<style scoped>
.app {
  font-family: 'Dosis', sans-serif;
  text-align: center;
  color: #E72C70;
}

.donut-cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  margin: 0 auto;
  width: 100%;
  max-width: 1200px;
}

</style>
