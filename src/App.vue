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
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>
