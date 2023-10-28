<script setup lang="ts">
import UserLocation from './components/UserLocation.vue'
import Map from './components/Map.vue'

const t = [1, 2, 3]
const fetchEvents = async() =>{
    const clientID = "yJwWTL9ZIxBdwB74S77pX"
    const clientSecret = "rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg"
    const res = await fetch('https://api.aerisapi.com/fires/within?p=edmonton,ab&format=json&client_id=yJwWTL9ZIxBdwB74S77pX&client_secret=rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg&limit=250&radius=1000km')
    return await res.json()
}
const events = fetchEvents();
console.log(events)

</script>

<template>
    <Map>
        <div v-for="event in events" :lat="event.loc.lat" :lng="event.loc.long">HELLO</div>
    </Map>
</template>

<style>
#app{
    width: 100vw;
    height: 100vh;
    padding: 0 !important;
    margin: 0 !important;
    max-width: none;
}
</style>
