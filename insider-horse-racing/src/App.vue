<script setup>

import { useRaceStore } from '../stores/raceStore';
import { ref } from 'vue';

const raceStore = useRaceStore()
const horseListOpen = ref(true)
const resultListOpen = ref(true)

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

    <button class="race-buttons" v-if="raceStore.raceStatus === 'idle' && raceStore.horses.length > 0" @click="raceStore.startTournament">Start Tournament</button>

    <aside class="race-results" v-if="raceStore.racingHorses.length > 0">
      <button v-if="raceStore.raceResults.length > 0" class="toggle-result-list" @click="resultListOpen = !resultListOpen">◰</button>
      <div v-if="resultListOpen" v-for="raceResult in raceStore.raceResults">
        <h3>Race {{ raceResult.raceId }} - {{ raceResult.distance }} m</h3>
        <ol>
          <li v-for="horse in raceResult.raceResult" :key="horse.id">
            <span class="color-name" :style="{ color: horse.color.value}">
              ■
            </span>
            Horse #{{ horse.id }}
          </li>
        </ol>
      </div>
    </aside>
    <section class="race-board">
      <div class="race-lane" v-for="horse in raceStore.racingHorses" :key="horse.id">
        <div class="lane-label">
          <span class="color-name" :style="{ color: horse.color.value}">
            ■
          </span>
          #{{ horse.id }}
        </div>
        <div class="lane-tiles" :style="{'--tile-count': raceStore.raceTiles.length}">
          <div v-for="tile in raceStore.raceTiles" :key="tile.id" class="tile-type" :class="tile.type" >
          </div>
          <div class="horse-sprite" :style="{
            '--horse-color': horse.color.value,
            left: `${((raceStore.horsePositions[horse.id] ?? 0) / raceStore.raceTiles.length) * 100}%`
          }">
          <img class="horse-outline" src="/horse_outline.png" alt="">
          </div>
        </div>
      </div>
    </section>

    <button class="race-buttons" v-if="raceStore.raceStatus === 'tournamentFinished'" @click="raceStore.startTournament">Restart Tournament</button>
    <button class="race-buttons" v-if="raceStore.raceStatus === 'running'" @click="raceStore.skipRace">▶▶ Skip Race</button>
    <button class="race-buttons" v-if="raceStore.raceStatus === 'ready'" @click="raceStore.runCurrentRace">Start Race</button>
    <button class="race-buttons" v-if="raceStore.raceStatus === 'finished'" @click="raceStore.nextRace">Next Race</button>
  </main>

</template>
