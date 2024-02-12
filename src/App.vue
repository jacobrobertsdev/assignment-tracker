<script setup>
import ClearAssignments from './components/ClearAssignments.vue';
import AddAssignmentForm from './components/AddAssignmentForm.vue'
import AssignmentList from './components/AssignmentList.vue'
import { ref, onMounted, watch } from 'vue'


const assignmentsList = ref([])


onMounted(() => {
assignmentsList.value = JSON.parse(localStorage.getItem('assignments')) || []
});

watch(assignmentsList, (updatedList) => {
    localStorage.setItem('assignments', JSON.stringify(updatedList))
})

function handleAddAssignment(newAssignment) {
    assignmentsList.value = [...assignmentsList.value, newAssignment]
}

function handleDeleteAssignment(id) {
    assignmentsList.value = assignmentsList.value.filter(assignment => assignment.id !== id)
}

function handleClearAssignments() {
    assignmentsList.value = []
}

</script>

<template>
<ClearAssignments @clearAll="handleClearAssignments"></ClearAssignments>
<AddAssignmentForm @addNewAssignment="handleAddAssignment"></AddAssignmentForm>
<AssignmentList @deleteAssignment="handleDeleteAssignment" :assignments="assignmentsList"></AssignmentList>

</template>

<style scoped>

</style>
