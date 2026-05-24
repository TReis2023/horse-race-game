<script setup>

import { useRaceStore } from '../stores/raceStore';
import { ref } from 'vue';

const raceStore = useRaceStore()
const horseListOpen = ref(true)

</script>

<template>
  <main>
    <h1>Horse Racing Game</h1>
    <aside class="all-horse">
      <button class="toggle-horse-list" @click="horseListOpen = !horseListOpen">◰</button>
      <button @click="raceStore.generateHorses">Generate Horses</button>
      <ul v-if="horseListOpen">
        <li v-for="horse in raceStore.horses" :key="horse.id">
          Horse #{{ horse.id }} |
          Color: 
          <span class="color-name" :style="{ color: horse.color.value}">
            ■
          </span>
          {{ horse.color.name }} |
          Condition: {{ horse.condition }}
        </li>
      </ul>
    </aside>


    <aside class="race-horse" v-if="raceStore.horses.length > 0">
      <button @click="raceStore.chooseHorses">Choose Racing Horses</button>
      <ul class="race-horse-list">
        <li v-for="raceHorse in raceStore.racingHorses" :key="raceHorse.id">
          Horse #{{ raceHorse.id }} 
          Color: 
          <span class="color-name" :style="{ color: raceHorse.color.value}">
            ■
          </span>
          {{ raceHorse.color.name }}
        </li>
      </ul>
    </aside>

    <aside class="race">
      <button @click="raceStore.simulateRaces">Start Race</button>
      <div v-for="raceResult in raceStore.raceResults">
        <h3>Race {{ raceResult.raceId }} - {{ raceResult.distance }} m</h3>
        <li v-for="horse in raceResult.raceResult" :key="horse.id">
          Horse {{ horse.id }}
        </li>
      </div>
    </aside>

  </main>

</template>
