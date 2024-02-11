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
        <p>Use the form to add your first assignment!</p>
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

div {
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