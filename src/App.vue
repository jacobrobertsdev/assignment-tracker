<script setup>
import ClearAssignments from './components/ClearAssignments.vue';
import AddAssignmentForm from './components/AddAssignmentForm.vue'
import AssignmentList from './components/AssignmentList.vue'
import CountMessage from './components/CountMessage.vue'
import CurrentDateDisplay from './components/CurrentDateDisplay.vue'
import { ref, onMounted, watch, computed } from 'vue'


const assignmentsList = ref([])

const count = computed(() => {
    return assignmentsList.value.length
})
onMounted(() => {
assignmentsList.value = JSON.parse(localStorage.getItem('assignments')) || []
});

watch(assignmentsList, (updatedList) => {
    localStorage.setItem('assignments', JSON.stringify(updatedList))
})

function handleAddAssignment(newAssignment) {
    assignmentsList.value = [ newAssignment,...assignmentsList.value]
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
<CurrentDateDisplay></CurrentDateDisplay>
<CountMessage :count="count"></CountMessage>
<AssignmentList @deleteAssignment="handleDeleteAssignment" :assignments="assignmentsList"></AssignmentList>

</template>

<style scoped>

</style>
