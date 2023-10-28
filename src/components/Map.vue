<template>
    <div class="map">
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
                v-for="event in events"
                :options="{
                    position: { lat: event.loc.lat, lng: event.loc.long },
                }"
            />
        </GoogleMap>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { GoogleMap, Marker } from 'vue3-google-map'

const props = defineProps<{
    range: number
    difficulty: number
    severity: number
    center: { lat: number; lng: number }
    city: string
    country: string
}>()

var events: any = []

const fetchEvents = async () => {
    const clientID = 'yJwWTL9ZIxBdwB74S77pX'
    const clientSecret = 'rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg'
    const res = await fetch(
        `https://api.aerisapi.com/fires/within?p=${props.city},ca&format=json&client_id=yJwWTL9ZIxBdwB74S77pX&client_secret=rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg&limit=250&radius=3000km`
    )
    const e = await res.json()
    events = e.response

    console.log(events)
}
fetchEvents()
</script>

<style scoped></style>
