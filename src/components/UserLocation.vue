<script setup lang="ts">
import { ref } from 'vue'
import { getCoords } from '../composables/location'
import { city_names } from '../data/cities'

const location = ref('Edmonton')
const showButtons = ref(true)
const enterLocation = ref(false)

const getUserLocation = () => {
    console.log('test')
    getCoords()
    showButtons.value = false
}

const showEnterLocation = () => {
    enterLocation.value = true
    showButtons.value = false
}
</script>

<template>
    <div class="user-location">
        <div
            v-if="showButtons"
            class="buttons"
        >
            <v-btn
                @click="getUserLocation"
                variant="outlined"
                >Use Your Location</v-btn
            >
            <v-btn
                @click="showEnterLocation"
                variant="outlined"
                >Enter Location</v-btn
            >
        </div>
    </div>
    <div
        v-if="enterLocation"
        class="enter-location"
    >
        <div class="helper">Enter Your Location:</div>
        <v-autocomplete
            :items="city_names"
            placeholder="Edmonton"
        ></v-autocomplete>
        <v-btn>OK</v-btn>
    </div>
</template>

<style scoped>
.user-location {
    .buttons {
        display: flex;
        flex-direction: column;
        gap: 20px;
        font-size: 48px;
    }
}

.enter-location {
    width: 300px;
}
</style>
