<script setup lang="ts">
import { ref } from 'vue'
import { getCoords } from '../composables/location'
import { cities } from '../data/cities'

import Map from './Map.vue'
import Controls from './Controls.vue'

const city = ref('')
const country = ref('')
const showButtons = ref(true)
const showEnterLocation = ref(false)
const showMap = ref(false)

const range = ref(0)
const difficulty = ref(0)
const severity = ref(0)

const center = ref({ lat: 53, lng: -113 })

const updateRange = (r: number) => {
    range.value = r
}
const updateDifficulty = (d: number) => {
    difficulty.value = d
}
const updateSeverity = (s: number) => {
    severity.value = s
}

const onGetUserLocation = () => {
    console.log('test')
    getCoords()
    city.value = 'Edmonton'
    country.value = 'Canada'
    showButtons.value = false
    showMap.value = true
}

const onShowshowEnterLocation = () => {
    showEnterLocation.value = true
    showButtons.value = false
}

const onOK = () => {
    showEnterLocation.value = false
    showMap.value = true

    if (city.value == 'Toronto') {
        center.value = { lat: 43, lng: -79 }
    }
    if (city.value == 'Beijing') {
        center.value = { lat: 40, lng: 116 }
    }
    if (city.value == 'Vancouver') {
        center.value = { lat: 49, lng: -123 }
    }
}
</script>

<template>
    <div class="user-location">
        <div
            v-if="showButtons"
            class="buttons"
        >
            <v-btn
                @click="onGetUserLocation"
                variant="outlined"
                >Use Your Location</v-btn
            >
            <v-btn
                @click="onShowshowEnterLocation"
                variant="outlined"
                >Enter Location</v-btn
            >
        </div>

        <div
            v-if="showEnterLocation"
            class="enter-location"
        >
            <div class="helper">Enter Your Location:</div>
            <v-autocomplete
                v-model="city"
                label="City"
                :items="cities"
                placeholder="Edmonton"
            ></v-autocomplete>
            <v-autocomplete
                v-model="country"
                label="Country"
                :items="['Canada', 'USA', 'Mexico', 'China']"
                placeholder="Edmonton"
            ></v-autocomplete>
            <v-btn @click="onOK">OK</v-btn>
        </div>
        <div
            v-if="showMap"
            class="map"
        >
            <Controls
                :range="range"
                :difficulty="difficulty"
                :severity="severity"
                @range="updateRange"
                @difficulty="updateDifficulty"
                @severity="updateSeverity"
            ></Controls>
            <Map
                :range="range"
                :difficulty="difficulty"
                :severity="severity"
                :center="center"
                :city="city"
                :country="country"
            ></Map>
        </div>
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

    .enter-location {
        width: 300px;

        .helper {
            padding: 20px;
        }
    }

    .map {
        display: flex;
        flex-direction: column;
    }
}
</style>
