<script setup lang="ts">
  import { reactive, toRaw } from 'vue'
  import { inject } from 'vue'
  import SearchBar from './SearchBar.vue'

  const axios: any = inject('axios')

  const state = reactive({
    city: null as any | null,
    loaded: false,
    error: false,
    errorMsg: ''
  });

  async function getWeather(selectedCity: String): Promise<void> {
    state.city = null
    state.loaded = false
    state.error = false
    state.errorMsg = ''
    // API Request
    try {
      const response = await axios.get(`http://api.openweathermap.org/data/2.5/weather`, {
        params: {
          q: selectedCity,
          units: 'metric',
          lang: 'fr',
          APPID: import.meta.env.VITE_OPENWEATHER_API_KEY
        }
      });
      console.log("API response : ", response.data)
      state.city = response.data
      toRaw(state.city)
      console.log("Local variable : ", state.city)
    } catch (err) {
      state.error = true
      state.errorMsg = err
      console.error("Erreur lors de la récupération des données Openweather : ",  err)
    }
    state.loaded = true
  }
</script>

<template>
  <SearchBar @selectedCity="getWeather" />

  <transition-group name="weather" tag="div">

    <div v-if="state.loaded && state.city && state.error == false">
      <h1>{{ state.city.name }}, {{ state.city.sys.country }}</h1>
      <img :src="'http://openweathermap.org/img/w/' + state.city.weather[0].icon + '.png'" alt="City weather image">
      <h2>{{ state.city.weather[0].description }}</h2>
      <h2>Humidité : {{ state.city.main.humidity }}%</h2>
      <h2>Température : {{ Math.round(state.city.main.temp) }}°C</h2>
      <h3>Ressenti : {{ Math.round(state.city.main.feels_like) }}°C</h3>
    </div>

    <div v-if="state.error">
      <h2 style="color: #a3160b;">Erreur lors de la récupération des données (vérifiez que le nom indiqué existe)</h2>
      <p>{{ state.errorMsg }}</p>
    </div>
    
  </transition-group>
</template>

<style scoped>
  template {
    display: flex;
    place-items: center;
  }

  .weather-enter-active, .weather-leave-active {
    transition: all 0.6s ease;
  }

  .weather-enter-from, .weather-leave-to {
    opacity: 0;
    transform: translateY(20px)
  }
</style>
