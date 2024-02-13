<script setup>
import Swal from 'sweetalert2'

const props = defineProps({
  assignments: Array
})

const emit = defineEmits(['clearAll'])

function handleClear() {

if (props.assignments.length){Swal.fire({
  title: "Clear all assignments?",
  text: "This will permanently delete all of your current assignments",
  icon: "question",
  showCancelButton: true,
  confirmButtonColor: "#1c7ed6",
  cancelButtonColor: "#d33",
  confirmButtonText: "Confirm",
  }).then((result) => {

  if (result.isConfirmed) {
    emit('clearAll')
    Swal.fire({
      title: "Deleted!",
      text: "Your assignments have been deleted.",
      icon: "success",
      confirmButtonColor: "#1c7ed6",
    })
  }
})

} else {
  Swal.fire({
    text: "No assignments to clear!",
    icon: "warning",
    confirmButtonColor: "#1c7ed6",
  })

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
    padding:.4rem;
    border: none;
    background-color: #1c7ed6;
    border-radius:5px;
}

</style>