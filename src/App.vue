<script setup>
import GbaPlayer from './components/GbaPlayer.vue';
import GameChooser, { eventTarget } from './components/GameChooser.vue';
//wimport HelloWorld from './components/HelloWorld.vue'
</script>

<script>
export default {
  data() {
    return {
      currentRomPath: null
    }
  },
  mounted() {
    eventTarget.addEventListener("loadgame", (ev) => {
      console.log(ev);
      this.currentRomPath = ev.detail;
    })
  }
}
</script>

<template>
    <GbaPlayer v-if="this.currentRomPath" :rom-name="this.currentRomPath"></GbaPlayer>
    <GameChooser :rom-path="this.currentRomPath" v-else></GameChooser>
</template>
