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
    <p>{{ name }}</p>
    <span class="course-name">{{ course }}</span>
    <span class="due-date">{{ due }}</span>
    <button class="delete" @click="deleteAssignment(id)">Delete</button>
</div>
</template>

<style scoped>
  .assignment{
        background-color:#122034;
        position: relative;
        padding: 2rem 1rem;
        width: 90%;
        border-radius: 5px;
        word-break: break-all;
    }

    span {
        font-size: .8rem;
    }

    .course-name {
        position: absolute;
        top:0;
        left:0;
        padding: .2rem .4rem;
        background-color: #4a5c75;
        color: white;
        border-bottom-right-radius: 5px;
        border-top-left-radius: 5px;

    }
    .due-date {
        position: absolute;
        top:0;
        right:0;
        padding: .2rem .4rem;
        background-color: #4a586c;
        color: white;
        border-bottom-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    .delete {
        font-size: .9rem;
        position: absolute;
        bottom:0;
        right:0;
        padding: .4rem;
        background-color: transparent;
        border: none;
        border-top-left-radius: 5px;
        border-bottom-right-radius: 5px;
        color: red;
    }

    .delete:hover{
        background-color: #48566a;
    }
</style>