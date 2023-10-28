<template>
    <div class="map">
        <v-card
            class="card"
            v-if="showDetails"
        >
            <v-card-title>
                {{ selectedEvent.id }}
            </v-card-title>
            <v-card-subtitle>
                {{
                    (
                        selectedEvent.place.name +
                        ',' +
                        selectedEvent.place.state +
                        ',' +
                        selectedEvent.place.country
                    ).toUpperCase()
                }}
            </v-card-subtitle>
            <v-card-subtitle>
                {{ selectedEvent.loc.lat + ' ' + selectedEvent.loc.long }}
            </v-card-subtitle>
            <v-card-text>
                <div>{{ 'Cause: ' + selectedEvent.report.cause }}</div>
                <div>
                    {{ 'Fire Range: ' + selectedEvent.report.areaKM + 'km^2' }}
                </div>
                <div>
                    {{
                        'Containment Percentage: ' +
                        selectedEvent.report.conf +
                        '%'
                    }}
                </div>
            </v-card-text>
        </v-card>
        <GoogleMap
            api-key="AIzaSyDzhSt4jyXKEkk5GRBUkNBaeRmoPIzbAPo"
            :style="{
                width: '75vw',
                height: '75vh',
            }"
            :center="center"
            :zoom="6"
        >
            <Marker
                @click="details(event)"
                style="color: blue"
                v-for="event in events"
                :options="{
                    position: { lat: event.loc.lat, lng: event.loc.long },
                    icon: getColor(event.report.areaKM),
                }"
            />
        </GoogleMap>
    </div>
</template>

<script setup lang="ts">
import { GoogleMap, Marker } from 'vue3-google-map'
import { ref } from 'vue'
import flameRed from '../assets/flameRed.svg' // Replace with the actual path
import flameOrange from '../assets/flameOrange.svg' // Replace with the actual path
import flameYellow from '../assets/flameYellow.svg' // Replace with the actual path
import flameGreen from '../assets/flameGreen.svg' // Replace with the actual path
import flameWhite from '../assets/flameWhite.svg' // Replace with the actual path

const props = defineProps<{
    city: string
    country: string
    center: { lat: number; lng: number }
}>()

const selectedEvent = ref()
const showDetails = ref(false)
const getColor = (km: number) => {
    if (km < 200) {
        return flameGreen
    }
    if (km < 400) {
        return flameYellow
    }
    if (km < 600) {
        return flameOrange
    }
    if (km < 800) {
        return flameRed
    }
    return flameWhite
}
const details = (event: any) => {
    selectedEvent.value = event
    showDetails.value = !showDetails.value
    console.log(event)
}
var events: any = []

const fetchEvents = async () => {
    const clientID = 'yJwWTL9ZIxBdwB74S77pX'
    const clientSecret = 'rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg'
    const res = await fetch(
        'https://api.aerisapi.com/fires/within?p=' +
            props.city +
            ',' +
            props.country +
            '&format=json&client_id=yJwWTL9ZIxBdwB74S77pX&client_secret=rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg&limit=250&radius=1000km'
    )
    const e = await res.json()
    events = e.response

    console.log(events)
}
fetchEvents()
</script>

<style scoped>
.card {
    position: absolute !important;
    width: 15% !important;
    height: 25% !important;
    z-index: 1000;
    top: 40%;
    right: 10%;
}
</style>
