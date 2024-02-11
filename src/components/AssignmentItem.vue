<script setup>
defineProps({
    course: String,
    name: String,
    due: String,
    id: String
});

const emit = defineEmits(['deleteAssignment'])

function deleteAssignment(id) {
    emit('deleteAssignment', id)
}

</script>

<template>
<div class="assignment">
    <h3>{{ name }}</h3>
    <span class="course-name">{{ course }}</span>
    <span class="due-date">Due: {{ due }}</span>
    <button class="delete" @click="deleteAssignment(id)">Delete</button>
</div>
</template>

<style scoped>
</style>