<script setup lang="ts">
  import WeatherSearch from './components/WeatherSearch.vue'
</script>

<template>
  <div>
    <img src="./assets/nuageux.png" class="logo vue" alt="Weatherapp logo" />
  </div>
  <WeatherSearch />

  <div class="credit">
    <p>
      Made by
      <a href="https://github.com/SebWayz" target="_blank" rel="noopener noreferrer">
        SebWay
      </a>
    </p>
    <p>
      Pluie icônes créées par 
      <a href="https://www.flaticon.com/fr/icones-gratuites/pluie" title="pluie icônes">iconixar - Flaticon</a>
    </p>
  </div>
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

  .credit {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 999;
    font-size: 13px;
  }

  .credit > a {
    text-decoration: none;
  }
</style>
