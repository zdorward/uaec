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

const onGetUserLocation = () => {
    console.log('test')
    getCoords()
    showButtons.value = false
}

const onShowshowEnterLocation = () => {
    showEnterLocation.value = true
    showButtons.value = false
}

const onOK = () => {
    showEnterLocation.value = false
    showMap.value = true
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
            :items="['Canada', 'USA', 'Mexico']"
            placeholder="Edmonton"
        ></v-autocomplete>
        <v-btn @click="onOK">OK</v-btn>
    </div>
    <div v-if="showMap">
        <Map
            :city="city"
            :country="country"></Map>
        <Controls
            city="Edmonton"
            country="Canada"
        ></Controls>
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

    .helper {
        padding: 20px;
    }
}
</style>
