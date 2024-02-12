<script setup>
import ClearAssignments from './components/ClearAssignments.vue';
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

function handleClearAssignments() {
    assignmentsList.value = []
    setLocalStorage(assignmentsList.value)
}

</script>

<template>
<ClearAssignments @clearAll="handleClearAssignments"></ClearAssignments>
<AddAssignmentForm @addNewAssignment="handleAddAssignment"></AddAssignmentForm>
<AssignmentList @deleteAssignment="handleDeleteAssignment" :assignments="assignmentsList"></AssignmentList>

</template>

<style scoped>

</style>
