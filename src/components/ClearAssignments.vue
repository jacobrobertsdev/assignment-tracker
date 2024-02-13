<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['clearAll'])

function handleClear() {
  const confirmed = window.confirm("Clear all of your assignments?")
  if (confirmed) {
    emit('clearAll')
  }
}
</script>

<template>
    <button @click="handleClear">Clear</button>
</template>

<style scoped>
button {
    
    position: fixed;
    top:-5px;
    left: 5%;
    z-index: 10;
    color: white;
    padding:.5rem .6rem .4rem .6rem;
    border: none;
    background-color: hsl(220, 75%, 45%);
    border-radius:5px
}

button:hover{
   background-color: hsl(220, 20%, 30%);
   color: white;
}
</style>