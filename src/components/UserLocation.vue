<script setup lang="ts">
import { ref } from 'vue'
import { getCoords } from '../composables/location'

const getUserLocation = () => {
    console.log('test')
    getCoords()
}

const count = ref(0)
</script>

<template>
    <div class="user-location">
        <v-btn @click="getUserLocation" variant="outlined"
            >Use Your Location</v-btn
        >
        <v-btn @click="console.log('test')" variant="outlined"
            >Enter Location</v-btn
        >
    </div>
</template>

<style scoped>
.user-location {
    display: flex;
    flex-direction: column;
    gap: 20px;
    font-size: 48px;
}
</style>
