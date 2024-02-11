<script setup>
import { ref, defineEmits } from 'vue'

const emit = defineEmits(['addNewAssignment'])

const formHidden = ref(true)
const courseName = ref('')
const assignmentName = ref('')
const dueDate = ref('')
const today = new Date().toISOString().split('T')[0]


function toggleForm() {
    formHidden.value = !formHidden.value
    courseName.value=''
    assignmentName.value = ''
    dueDate.value = ''
}



function addAssignment() {
   
   const newAssignment = {
       id: crypto.randomUUID().toString(),
       course: courseName.value,
       name: assignmentName.value,
       due: dueDate.value}

    emit('addNewAssignment', newAssignment)

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
            <input type="date" v-model="dueDate" name="due-date" id="due-date" :min="today" required>
        </section>
            
        <section class="controls">
            <button type="submit">Submit</button>
            <button @click="toggleForm">Cancel</button>
        </section>
            
        </form>
        
    </section>
   
</template>

<style scoped>
form {
    margin-bottom: 1rem;
    box-shadow: 0px 3px 7px -2px rgb(110, 110, 110);
    display: flex;
    flex-wrap: wrap;
    gap: .5rem;
    justify-content: center;
    align-items: center;
    padding: 1rem;
    border-radius: 12px;

}

.assignment-input, .due-date-input, .course-input, .controls {
    display: flex;
    gap: .5rem;
}
</style>