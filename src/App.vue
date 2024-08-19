<script setup>
import CardComponent from './components/CardComponent.vue'
</script>

<template>
  <div class="wrapper">
    <CardComponent />
  </div>
</template>

<style scoped>
  .wrapper {
    display: flex;
    justify-content: center;
    width: 100%;
    
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>
