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
    <h4>{{ name }}</h4>
    <span class="course-name">{{ course }}</span>
    <span class="due-date">{{ due }}</span>
    <button class="delete" @click="deleteAssignment(id)">Delete</button>
</div>
</template>

<style scoped>
  .assignment{
        background-color:white;
        box-shadow: 0px 3px 7px -2px rgb(110, 110, 110);
        position: relative;
        padding: 2rem 1rem;
        width: 90%;
        border-radius: 5px;
        word-break: break-all;

    }

    .course-name {
        position: absolute;
        top:0;
        left:0;
        padding: .2rem .3rem;
        background-color: rgb(119, 159, 136);
        color: white;
        border-bottom-right-radius: 5px;
        border-top-left-radius: 5px;

    }
    .due-date {
        position: absolute;
        top:0;
        right:0;
        padding: .2rem .3rem;
        background-color: rgb(119, 159, 136);
        color: white;
        border-bottom-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    .delete {
        position: absolute;
        bottom:0;
        right:0;
        padding: .2rem .3rem;
        background-color: rgb(219, 0, 0);
        border: none;
        border-top-left-radius: 5px;
        border-bottom-right-radius: 5px;
        color: white;
        cursor: pointer;
    }
</style>