<script setup lang="ts">
import { onMounted } from 'vue';
import { getCoords } from './composables/location';
getCoords();
</script>

<template>
    <v-btn>Button</v-btn>
</template>

<style scoped></style>
