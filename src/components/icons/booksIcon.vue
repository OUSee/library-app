<script setup>

const { width, height, color} = defineProps(["width","height","color"])
</script>


<template>
    <svg :width="width" :height="height" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path d="M4 10L12 6L20 10L12 14L4 10Z" :stroke="color" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M20 10V14" :stroke="color" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
        <path d="M7 12V17C7 17 7.45455 19 12 19C16.5455 19 17 17 17 17V12" :stroke="color" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
    </svg>
</template>