<script setup>
import { defineEmits } from 'vue';
import Swal from 'sweetalert2'

const emit = defineEmits(['clearAll'])

function handleClear() {
  // const confirmed = window.confirm("Clear all of your assignments?")
  // if (confirmed) {
  //   emit('clearAll')
  // }

  Swal.fire({
  title: "Clear all assignments?",
  text: "This will permanently delete all of your current assignments",
  icon: "warning",
  showCancelButton: true,
  confirmButtonColor: "#1c7ed6",
  cancelButtonColor: "#d33",
  confirmButtonText: "Confirm"
}).then((result) => {
  if (result.isConfirmed) {
  emit('clearAll')
  }
});
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
    color: white;
    padding:.4rem;
    border: none;
    background-color: #1c7ed6;
    border-radius:5px
}

button:hover{
   background-color: hsl(220, 20%, 30%);
   color: white;
}
</style>