<script setup>
import AssignmentItem from './AssignmentItem.vue';

defineProps({
    assignments: Array
})

const emit = defineEmits(['deleteAssignment']);

function handleDelete(id) {
    emit('deleteAssignment', id);
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

    <AssignmentItem v-else v-for="assignment in assignments" :key="assignment.id" 
    :name="assignment.name" 
    :course="assignment.course"
    :due="displayDueDate(assignment.due)" 
    :assignments="assignments"
    :id="assignment.id"
    @deleteAssignment="handleDelete">
    </AssignmentItem>
    </section>
</template>

<style scoped>


.assignments-list{
    margin:3rem auto;
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
    padding: 6rem 4rem;
    max-width: 90%;
    margin: 6rem auto;
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