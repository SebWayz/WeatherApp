<script setup lang="ts">
  import WeatherSearch from './components/WeatherSearch.vue'
</script>

<template>
  <div>
    <img src="./assets/nuageux.png" class="logo vue" alt="Weatherapp logo" />
  </div>
  <WeatherSearch />
</template>

<style scoped>
  .logo {
    height: 12em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #870ff7);
  }
</style>
