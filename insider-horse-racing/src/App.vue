<script setup>
import { useRaceStore } from '../stores/raceStore';

const raceStore = useRaceStore()

</script>

<template>
  <main>
    <h1>Horse Racing Game</h1>
    <button @click="raceStore.generateHorses">Generate Horses</button>
    <ul>
      <li v-for="horse in raceStore.horses" :key="horse.id">
        Horse {{ horse.id }} |
        Color: {{ horse.color.name }} |
        Condition: {{ horse.condition }}
      </li>
    </ul>
  </main>

</template>
