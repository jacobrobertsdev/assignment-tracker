<script setup>
import { ref } from 'vue'

const emit = defineEmits(['addNewAssignment'])

const formHidden = ref(true)
const courseName = ref('')
const assignmentName = ref('')
const dueDate = ref('')
const today = new Date().toISOString().split('T')[0]


function toggleForm() {
    courseName.value=''
    assignmentName.value = ''
    dueDate.value = ''
    formHidden.value = !formHidden.value
}

function addAssignment() {
   const newAssignment = {
       id: crypto.randomUUID().toString(),
       course: courseName.value,
       title: assignmentName.value,
       due: dueDate.value}

    emit('addNewAssignment', newAssignment)
    toggleForm()
}

</script>

<template>
    
    <button v-if="formHidden" @click="toggleForm" class="add-assignment">+Add</button>

    <section class="assignment-form">

        <form v-if="!formHidden" id="new-assignment" name="New Assignment Form" @submit.prevent="addAssignment">

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

            <button>Submit</button>
            <button @click="toggleForm" type="button">Cancel</button>
        </section>

        </form>
    </section>
   
</template>

<style scoped>

form {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    justify-content: center;
    align-items: center;
    background-color: var(--background);
    z-index: 20;

}

.controls{
    margin-top: .5rem;
    display: flex;
    align-self: center;
    gap: 1rem;
}

form button {
    background-color: var(--background);
    padding:.4rem .6rem;
    border: 1px solid white;
    border-radius:5px
}

label{
    margin-left: .1rem;
}

input {
    width: 15rem;
    height: 2.1rem;
    padding: .4rem;
    border-radius: 5px;
}

.add-assignment {
    position: fixed;
    top:3%;
    right: 5%;
    z-index: 10;
    padding:.4rem;
    border: none;
    background-color: #1c7ed6;
    border-radius:5px
}

.assignment-input, .due-date-input, .course-input {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: .3rem;
}

button:hover {
  background-color: hsl(220, 20%, 30%);
}
</style>