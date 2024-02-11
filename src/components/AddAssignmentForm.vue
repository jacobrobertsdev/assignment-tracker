<script setup>
import { ref, defineEmits, onMounted } from 'vue'

const emit = defineEmits(['addNewAssignment'])

const formHidden = ref(true)
const courseName = ref('')
const assignmentName = ref('')
const dueDate = ref('')
const minDate = ref('')

onMounted(() => {
      // Set  minimum date to current date
      const today = new Date().toISOString().split('T')[0]
      minDate.value = today
});

function toggleForm() {
    formHidden.value = !formHidden.value
}

function formatDate(dateStr) {
    const parts = dateStr.split('-')
    const year = parts[0]
    const month = parts[1]
    const day = parts[2]
    return `${month}/${day}/${year}`
}

function addAssignment() {
   
   const newAssignment = {
       id: crypto.randomUUID().toString(),
       course: courseName.value,
       name: assignmentName.value,
       due: formatDate(dueDate.value)}

    emit('addNewAssignment', newAssignment)
   
    assignmentName.value = ''
    dueDate.value = ''

    toggleForm()
}

</script>

<template>
    
    <button v-if="formHidden" @click="toggleForm" class="add-assignment"> + Add Assignment</button>

    <section class="assignment-form">
        <form v-if="!formHidden" @submit.prevent="addAssignment">
        <section class="course-input">
            <label for="course">Course:</label>
            <input type="text" v-model="courseName" name="course" id="course" placeholder="Course name..." maxlength="20" required>
        </section>

        <section class="assignment-input">
            <label for="assignment">Assignment:</label>
            <input type="text" v-model="assignmentName" name="Assignment" id="assignment" placeholder="New assignment..." required>
        </section>
            
        <section class="due-date-input">
            <label for="due-date">Due Date:</label>
            <input type="date" v-model="dueDate" name="due-date" id="due-date" :min="minDate" required>
        </section>
            
        <section class="controls">
            <button type="submit">Submit</button>
            <button @click="toggleForm">Cancel</button>
        </section>
            
        </form>
        
    </section>
   
</template>

<style scoped>
</style>