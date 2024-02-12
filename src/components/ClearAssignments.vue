<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['clearAll'])

function handleClear() {
  const confirmed = window.confirm("Clear all of your assignments?");
  if (confirmed) {
    emit('clearAll');
  }
}
</script>

<template>
    <button @click="handleClear">Clear</button>
</template>

<style scoped>
button {
    position: fixed;
    top:5%;
    left: 5%;
    z-index: 10;
}
</style>