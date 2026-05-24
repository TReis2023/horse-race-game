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
      <button v-if="raceStore.horses.length === 0" @click="raceStore.generateHorses">Generate Horses</button>
      <ul class="full-horse-list" v-if="horseListOpen">
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
      <button v-if="raceStore.raceStatus === 'idle'" @click="raceStore.startTournament">Start Tournament</button>
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

    <aside class="race-results" v-if="raceStore.racingHorses.length > 0">
      <button v-if="raceStore.raceStatus === 'ready'" @click="raceStore.runCurrentRace">Start Race</button>
      <button v-if="raceStore.raceStatus === 'finished'" @click="raceStore.nextRace">Next Race</button>
      <div v-for="raceResult in raceStore.raceResults">
        <h3>Race {{ raceResult.raceId }} - {{ raceResult.distance }} m</h3>
        <li v-for="horse in raceResult.raceResult" :key="horse.id">
          Horse {{ horse.id }}
        </li>
      </div>
    </aside>
    <section class="race-board">
      <div class="race-lane" v-for="horse in raceStore.racingHorses" :key="horse.id">
        <div class="lane-label">
          #{{ horse.id }}
        </div>
        <div class="lane-tiles" :style="{'--tile-count': raceStore.raceTiles.length}">
          <div v-for="tile in raceStore.raceTiles" :key="tile.id" class="tile-type" :class="tile.type" >
            {{ tile.type }}
          </div>
        </div>
      </div>
    </section>

    <button class="restart-button" v-if="raceStore.raceStatus === 'tournamentFinished'" @click="raceStore.startTournament">Restart Tournament</button>

  </main>

</template>
