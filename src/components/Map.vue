<template>
  <GoogleMap api-key="AIzaSyDzhSt4jyXKEkk5GRBUkNBaeRmoPIzbAPo" style="width: 100%; height: 100%" :center="center" :zoom="10">
    <Marker v-for="event in events" :options="{ position: {lat: event.loc.lat, lng: event.loc.long} }" />
  </GoogleMap>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";
const fetchEvents = async() =>{
    const clientID = "yJwWTL9ZIxBdwB74S77pX"
    const clientSecret = "rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg"
    const res = await fetch('https://api.aerisapi.com/fires/within?p=edmonton,ab&format=json&client_id=yJwWTL9ZIxBdwB74S77pX&client_secret=rzE1z8DJhQtmuDzJCNKyjCoBbOtZ27LpfBl8OHOg&limit=250&radius=1000km')
    return await res.json()
}
const events = fetchEvents();


export default defineComponent({
  components: { GoogleMap, Marker },
  setup() {

    const center = { lat: 53.5232, lng: -113.18 }

    return { center };
  },
});
</script>
