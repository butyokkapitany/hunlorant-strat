<template>
  <Strat/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Strat from './components/StratRoulette.vue';

export default defineComponent({
  name: 'App',
  components: {
    Strat,
  },
});
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap');
@font-face {
  font-family: Valorant;
  src: url("valorant_font.ttf");
}

:root {
  --background: hsl(0, 0%, 7%);
  --text: hsl(36, 100%, 98%);
  --accent1: hsl(348, 43%, 23%);
  --accent2: hsl(355, 54%, 48%);
  --accent3: hsl(354, 98%, 63%);
  --accent4: hsl(216, 31%, 31%);
}
body {
  background-color: var(--background);
  color: var(--text);
  font-family: 'Roboto Condensed', sans-serif;
}
</style>
