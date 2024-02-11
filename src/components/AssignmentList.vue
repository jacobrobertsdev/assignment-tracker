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
    const currentDateString = currentDate.toISOString().split('T')[0]; // Extract date string without time component

    const due = new Date(dueDate);
    const dueDateString = due.toISOString().split('T')[0]; 

    const tomorrow = new Date(currentDate);
    tomorrow.setDate(currentDate.getDate() + 1);
    const tomorrowDateString = tomorrow.toISOString().split('T')[0];

    if (dueDateString === currentDateString) {
        return 'Due today!';
    } else if (dueDateString === tomorrowDateString) {
        return 'Due tomorrow';
    } else if (due < currentDate) {
        return 'Past due';
    } else {
        return `Due: ${formatDate(dueDate)}`;
    }
}
</script>

<template>

<section class="assignments-list">
    <div class="placeholder" v-if="assignments.length === 0">
        <p>Use the form to add your first assignment!</p>
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

.placeholder {
    padding: 3rem;
    margin: 1.5rem;
    text-align: center;
    border: 3px dashed rgba(111, 111, 111, 0.491);
    border-radius: 10px;

}
.assignments-list{
    margin-top: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    width:100%;
}

@media (min-width: 1000px){
    .assignments-list {
        width: 60%;
    }
}
</style>