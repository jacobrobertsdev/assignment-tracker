<script setup>
import { ref, defineEmits} from 'vue'

const props = defineProps({
    course: String,
    title: String,
    due: String,
    id: String
});

const emit = defineEmits(['deleteAssignment', 'editAssignment'])

const readOnly = ref(true)
const inputRef = ref(null)
const editedTitle = ref(props.title)


const toggleEdit = () => {
    readOnly.value = !readOnly.value

    if (!readOnly.value) {
        inputRef.value.focus()}
}

const preventFocus = (event) => {
  event.preventDefault()
}


function deleteAssignment() {
    emit('deleteAssignment', props.id)
}

function handleEditTitle(value) {
    editedTitle.value = value
}

function saveEdit() {
    toggleEdit()
    emit('editAssignment', { id:props.id, newTitle: editedTitle.value })
    
}

</script>

<template>
    <li class="assignment">

        <textarea rows="1"  name="assignment title" ref="inputRef" :readonly="readOnly" :value="editedTitle" :onmousedown="readOnly ? preventFocus : null " @change="handleEditTitle($event.target.value)"></textarea>

        <span class="course-name">{{ props.course }}</span>
        <span class="due-date">Due: {{ props.due }}</span>

        <button class="delete" @click="deleteAssignment">Delete</button>
        <button  v-if="readOnly" class="edit" @click="toggleEdit">Edit</button>
        <button  v-else class="save" @click="saveEdit">Save</button>

    </li>
</template>

<style scoped>
  .assignment{
        background-color:#122034;
        position: relative;
        padding: 2.8rem 1rem;
        width: 90%;
        border-radius: 5px;
        word-break: break-all;
    }

    textarea {
        width: 100%;
        background-color: transparent;
        color: var(--text);
        font-size: .9rem;
        border: none;
        resize: none;
    }

    textarea::-webkit-scrollbar {
        width: .6rem;
    }

    textarea::-webkit-scrollbar-track {
        background-color: var(--background);
        border-radius: 3px;
    }

    textarea::-webkit-scrollbar-thumb {
        background-color: #8390a3;
        border-radius: 3px;

    }
    span {
        font-size: .8rem;
    }

    .course-name {
        position: absolute;
        top:0;
        left:0;
        padding: .2rem .4rem;
        background-color: #495057;
        border-bottom-right-radius: 5px;
        border-top-left-radius: 5px;

    }
    .due-date {
        position: absolute;
        top:0;
        right:0;
        padding: .2rem .4rem;
        background-color: #495057;
        border-bottom-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    .delete {
        font-size: .9rem;
        position: absolute;
        bottom:0;
        right:0;
        padding: .2rem .4rem;
        background-color: transparent;
        border: none;
        border-top-left-radius: 5px;
        border-bottom-right-radius: 5px;
        color: red;
    }
    .edit, .save {
        font-size: .8rem;
        position: absolute;
        bottom:0;
        left:0;
        padding: .2rem .4rem;
        background-color: #1864ab;
        border: none;
        border-top-right-radius: 5px;
        border-bottom-left-radius: 5px;
       
    }

    button:hover {
    background-color: hsl(220, 20%, 30%);
    }
</style>