<script setup lang="ts">
import { ref } from 'vue'

defineProps<{ city: string; country: string }>()
const range = ref(0)
const difficulty = ref(0)
const severity = ref(0)
</script>

<template>
    <div class="controls">
        <div class="slider-container">
            <div class="slider">
                <v-slider
                    v-model="range"
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                ></v-slider>
            </div>
            <div class="name">Range of Fire: {{ range }}</div>
        </div>
        <div class="slider-container">
            <div class="slider">
                <v-slider
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                ></v-slider>
            </div>
            <div class="name">Difficulty to contain: {{ difficulty }}</div>
        </div>
        <div class="slider-container">
            <div class="slider">
                <v-slider
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                ></v-slider>
            </div>
            <div class="name">Severity of Fire: {{ severity }}</div>
        </div>
    </div>
</template>

<style scoped>
.controls {
    .slider-container {
        display: flex;
        .slider {
            width: 200px;
        }
    }
}
</style>
