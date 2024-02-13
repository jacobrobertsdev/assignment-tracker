<script setup>
import AssignmentItem from './AssignmentItem.vue'

const props = defineProps({
    assignments: Array
})

const emit = defineEmits(['deleteAssignment', 'editAssignment'])

function handleDelete(id) {
    emit('deleteAssignment', id)
}
function handleEdit(updatedAssignment) {
    emit('editAssignment', updatedAssignment)
}


function formatDate(dateStr) {
    const parts = dateStr.split('-')
    const year = parts[0]
    const month = parts[1]
    const day = parts[2]
    return `${month}/${day}/${year}`
}


</script>

<template>

<section class="assignments-list">
    <div class="placeholder" v-if="assignments.length === 0">
        <p>No assignments!</p>
    </div>

    <AssignmentItem v-else v-for="assignment in props.assignments" :key="assignment.id" 
    :title="assignment.title" 
    :course="assignment.course"
    :due="formatDate(assignment.due)" 
    :assignments="assignments"
    :id="assignment.id"
    @deleteAssignment="handleDelete"
    @editAssignment="handleEdit">
    </AssignmentItem>
    </section>
</template>

<style scoped>


.assignments-list{
    margin:0.5rem auto 2rem auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    width:100%;
}

.placeholder {
    text-align: center;
    opacity: .5;
    padding: 6rem 5rem;
    max-width: 90%;
    margin: 5rem auto;
    border: 2px dashed white;
    border-radius: 10px;
    z-index: -1;


}

@media (min-width: 1000px){
    .assignments-list {
        width: 60%;
    }
}
</style>