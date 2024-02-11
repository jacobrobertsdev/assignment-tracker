<script setup>
import AssignmentItem from './AssignmentItem.vue';

defineProps({
    assignments: Array
})

const emit = defineEmits(['deleteAssignment']);

function handleDelete(id) {
    emit('deleteAssignment', id);
}
</script>

<template>

<section class="assignments-list">
    <div v-if="assignments.length === 0">
        <h3>No assignments to show -</h3>
        <p>Use the form to add your next assignment!</p>
    </div>

    <AssignmentItem v-else v-for="assignment in assignments" :key="assignment.id" 
    :name="assignment.name" 
    :course="assignment.course"
    :due="assignment.due" 
    :assignments="assignments"
    :id="assignment.id"
    @deleteAssignment="handleDelete">
    </AssignmentItem>
    </section>
</template>

<style scoped>
</style>