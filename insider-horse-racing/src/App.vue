<script setup>
import HelloWorld from './components/HelloWorld.vue'
import { useRaceStore } from '../stores/raceStore';

const raceStore = useRaceStore()

</script>

<template>
  <main>
    <h1>Horse Racing Game</h1>
    <button>Generate Horses</button>
  </main>

</template>
