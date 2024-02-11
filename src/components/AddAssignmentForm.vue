<script setup>
import { ref, defineEmits, onMounted } from 'vue'

const emit = defineEmits(['addNewAssignment'])

const formHidden = ref(true)
const courseName = ref('')
const assignmentName = ref('')
const dueDate = ref('')
const minDate = ref('')

onMounted(() => {
      // Set  minimum date to current date
      const today = new Date().toISOString().split('T')[0]
      minDate.value = today
});

function toggleForm() {
    formHidden.value = !formHidden.value
}

function formatDate(dateStr) {
    const parts = dateStr.split('-')
    const year = parts[0]
    const month = parts[1]
    const day = parts[2]
    return `${month}/${day}/${year}`
}

function addAssignment() {
   
   const newAssignment = {
       id: crypto.randomUUID().toString(),
       course: courseName.value,
       name: assignmentName.value,
       due: formatDate(dueDate.value)}

    emit('addNewAssignment', newAssignment)
   
    assignmentName.value = ''
    dueDate.value = ''

    toggleForm()
}

</script>

<template>
</template>

<style scoped>
</style>