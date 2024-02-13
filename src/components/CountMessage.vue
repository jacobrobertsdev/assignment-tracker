<script setup>

const props = defineProps({
   count: Number 
})

</script>

<template>
    <h4 v-if="props.count === 1">You have {{ props.count }} assignment</h4>
    <h4 v-else-if="props.count > 1">You have {{ props.count }} assignments</h4>
</template>

<style scoped>

h4 {
    font-size: .9rem;
    margin-top: 2rem;
}

</style>