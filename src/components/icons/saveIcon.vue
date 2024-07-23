<template>
    <svg :width="width" :height="height" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path
            d="M58 43V48C58 49.8856 58 50.8284 57.4142 51.4142C56.8284 52 55.8856 52 54 52H44.5C43.1193 52 42 50.8807 42 49.5V49.5C42 48.1193 43.1193 47 44.5 47H54C55.8856 47 56.8284 47 57.4142 46.4142C58 45.8284 58 44.8856 58 43V38C58 36.1144 58 35.1716 57.4142 34.5858C56.8284 34 55.8856 34 54 34H46C44.1144 34 43.1716 34 42.5858 34.5858C42 35.1716 42 36.1144 42 38V49.5"
            :stroke="color" />
        <path d="M47 41L48.2929 42.2929C48.6834 42.6834 49.3166 42.6834 49.7071 42.2929L53 39" :stroke="color"
            stroke-linecap="round" />
    </svg>
</template>

<script setup>
const { width, height, color } = defineProps(["width", "height", "color"])
</script>
