<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['clearAll'])

function handleClear() {
    emit('clearAll')
}
</script>

<template>
    <button @click="handleClear">Clear All</button>
</template>