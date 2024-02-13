<script setup>
import AssignmentItem from './AssignmentItem.vue';

const props = defineProps({
    assignments: Array
})

const emit = defineEmits(['deleteAssignment', 'editAssignment']);

function handleDelete(id) {
    emit('deleteAssignment', id);
}
function handleEdit(updatedAssignment) {
    emit('editAssignment', updatedAssignment);
}


function formatDate(dateStr) {
    const parts = dateStr.split('-')
    const year = parts[0]
    const month = parts[1]
    const day = parts[2]
    return `${month}/${day}/${year}`
}

function displayDueDate(dueDate) {
    const currentDate = new Date();
    currentDate.setUTCHours(0, 0, 0, 0);

    const due = new Date(dueDate);
    due.setUTCHours(0, 0, 0, 0);

    if (due.getTime() === currentDate.getTime()) {
        return 'Due today!';
    } else if (due.getTime() < currentDate.getTime()) {
        return 'Past due';
    } else {
        return `Due: ${formatDate(dueDate)}`;
    }
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
    :due="displayDueDate(assignment.due)" 
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