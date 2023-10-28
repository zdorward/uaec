<script setup lang="ts">
import { ref, watch } from 'vue'

const props = defineProps<{
    range: number
    difficulty: number
    severity: number
}>()
const emit = defineEmits<{
    (e: 'range', id: number): void
    (e: 'difficulty', value: number): void
    (e: 'severity', value: number): void
}>()

const range = ref(props.range)
const difficulty = ref(props.difficulty)
const severity = ref(props.severity)

watch(range, (newRange) => {
    emit('range', newRange)
})
watch(difficulty, (newDifficulty) => {
    emit('difficulty', newDifficulty)
})
watch(severity, (newSeverity) => {
    emit('severity', newSeverity)
})
</script>

<template>
    <div class="controls">
        <div class="slider-container">
            <div class="slider">
                Range of Fire: {{ range }}
                <v-slider
                    v-model="range"
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                    show-ticks="always"
                    tick-size="4"
                ></v-slider>
            </div>
        </div>
        <div class="slider-container">
            <div class="slider">
                Difficulty to contain: {{ difficulty }}
                <v-slider
                    v-model="difficulty"
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                    show-ticks="always"
                    tick-size="4"
                ></v-slider>
            </div>
        </div>
        <div class="slider-container">
            <div class="slider">
                Severity of Fire: {{ severity }}
                <v-slider
                    v-model="severity"
                    thumb-label
                    min="0"
                    max="5"
                    step="1"
                    show-ticks="always"
                    tick-size="4"
                ></v-slider>
            </div>
        </div>
    </div>
</template>

<style scoped>
.controls {
    display: flex;
    .slider-container {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;
        .slider {
            width: 200px;
        }
    }
}
</style>
