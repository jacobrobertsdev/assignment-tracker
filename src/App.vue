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
}, {deep:true})


///Handler functions///
function handleAddAssignment(newAssignment) {
    assignmentsList.value = [ newAssignment,...assignmentsList.value]
}

function handleDeleteAssignment(id) {
    assignmentsList.value = assignmentsList.value.filter(assignment => assignment.id !== id)
}

function handleClearAssignments() {
    assignmentsList.value = []
}

function handleEditAssignment(updatedAssignment) {
    const index = assignmentsList.value.findIndex(item => item.id == updatedAssignment.id)
    if (index !== -1) {
        assignmentsList.value[index].title = updatedAssignment.newTitle;
    }
}
</script>

<template>

<ClearAssignments @clearAll="handleClearAssignments" :assignments="assignmentsList"></ClearAssignments>
<AddAssignmentForm @addNewAssignment="handleAddAssignment"></AddAssignmentForm>
<CurrentDateDisplay></CurrentDateDisplay>
<CountMessage :count="count"></CountMessage>
<AssignmentList @deleteAssignment="handleDeleteAssignment"
@editAssignment="handleEditAssignment" :assignments="assignmentsList">
</AssignmentList>

</template>

<style scoped>

</style>
