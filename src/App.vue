<script setup lang="ts">
import UserLocation from './components/UserLocation.vue'
import Controls from './components/Controls.vue'
</script>

<template>
    <UserLocation></UserLocation>
    <Controls
        city="Edmonton"
        country="Canada"
    ></Controls>
</template>

<style scoped></style>
