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
    top:3%;
    left: 5%;
    z-index: 10;
    background-color: var(--background);
    color: whitesmoke;
    padding:.4rem;
    border: 1px solid whitesmoke;
    border-radius:5px
}

button:hover{
   background-color: hsl(220, 20%, 30%);
   color: white;
}
</style>