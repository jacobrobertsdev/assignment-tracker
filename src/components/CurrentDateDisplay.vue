<template>
    <div>
      <h3>{{ formattedDateTime }}</h3>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const formattedDateTime = ref('');
  
  onMounted(() => {
    const now = new Date();
  
    const options = { 
      month: 'numeric', 
      day: 'numeric', 
      year: 'numeric', 
      hour: 'numeric', 
      minute: '2-digit' 
    };
  
    formattedDateTime.value = now.toLocaleDateString(undefined, options)
  });
  </script>
  
  <style scoped>
  h3 {
    font-size: 1rem;
  }
  </style>