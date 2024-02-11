<script setup>
import AddAssignmentForm from './components/AddAssignmentForm.vue'
import AssignmentList from './components/AssignmentList.vue'
import { ref, onMounted } from 'vue'


const assignmentsList = ref([])

onMounted(() => {
    const savedAssignments = localStorage.getItem('assignments') || []
    if (savedAssignments) assignmentsList.value = JSON.parse(savedAssignments)
})

function setLocalStorage(list) {
    localStorage.setItem('assignments', JSON.stringify(list))
}

function handleAddAssignment(newAssignment) {
    assignmentsList.value.push(newAssignment)
    setLocalStorage(assignmentsList.value)
}

function handleDeleteAssignment(id) {
    assignmentsList.value = assignmentsList.value.filter(assignment => assignment.id !== id)
    setLocalStorage(assignmentsList.value)
}

</script>

<template>

<AddAssignmentForm @addNewAssignment="handleAddAssignment"></AddAssignmentForm>
<AssignmentList @deleteAssignment="handleDeleteAssignment" :assignments="assignmentsList"></AssignmentList>

</template>

<style scoped>

</style>
