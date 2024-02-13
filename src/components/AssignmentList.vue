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

    <div class="placeholder" v-if="props.assignments.length === 0">
        <p>No assignments!</p>
    </div>
    <ul v-else>
    <AssignmentItem  v-for="assignment in props.assignments" :key="assignment.id" 
    :title="assignment.title" 
    :course="assignment.course"
    :due="formatDate(assignment.due)" 
    :assignments="props.assignments"
    :id="assignment.id"
    @deleteAssignment="handleDelete"
    @editAssignment="handleEdit">
    </AssignmentItem>
    </ul>
</section>

</template>

<style scoped>

ul {
    list-style-type: none;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 1rem;
    width:100%;
}
.assignments-list{
    margin:0.5rem auto 2rem auto;
    width: 100%;
}

.placeholder {
    text-align: center;
    opacity: .5;
    padding: 6rem 5rem;
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

    .placeholder {
    padding: 7rem 10rem;
    }
}
</style>