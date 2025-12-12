<script setup>
import { ref, onMounted } from 'vue'
import SearchBar from './components/SearchBar.vue'
import WeatherCard from './components/WeatherCard.vue'

const weatherData = ref(null)
const loading = ref(false)
const error = ref(null)

const getCoordinates = async (city) => {
  try {
    const response = await fetch(
      `https://geocoding-api.open-meteo.com/v1/search?name=${city}&count=1&language=en&format=json`
    )
    const data = await response.json()
    
    if (!data.results || data.results.length === 0) {
      throw new Error('City not found')
    }
    
    return data.results[0]
  } catch (err) {
    throw err
  }
}

const getWeather = async (lat, lon) => {
  try {
    const response = await fetch(
      `https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current_weather=true`
    )
    const data = await response.json()
    return data.current_weather
  } catch (err) {
    throw new Error('Failed to fetch weather data')
  }
}

const handleSearch = async (city) => {
  loading.value = true
  error.value = null
  weatherData.value = null
  
  try {
    const location = await getCoordinates(city)
    const weather = await getWeather(location.latitude, location.longitude)
    
    weatherData.value = {
      ...weather,
      name: location.name,
      country: location.country
    }
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

onMounted(() => {
  handleSearch('Monrovia')
})
</script>

<template>
  <main>
    <div class="header">
      <h1 class="title">Weather<span class="highlight">Dash</span></h1>
      <p class="subtitle">Check the weather anywhere, instantly.</p>
    </div>

    <SearchBar @search-city="handleSearch" />

    <div class="content-area">
      <div v-if="loading" class="loading-state">
        <div class="spinner"></div>
        <p>Fetching weather data...</p>
      </div>

      <div v-else-if="error" class="error-state glass-panel">
        <span class="error-icon">⚠️</span>
        <p>{{ error }}</p>
      </div>

      <WeatherCard 
        v-else-if="weatherData" 
        :weather="weatherData" 
      />
      
      <div v-else class="empty-state">
        <p>Enter a city name above to get started.</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.header {
  text-align: center;
  margin-bottom: 2rem;
}

.title {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  background: linear-gradient(to right, #fff, #a5b4fc);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.highlight {
  color: hsl(var(--color-primary-hsl));
  -webkit-text-fill-color: hsl(var(--color-primary-hsl));
}

.subtitle {
  color: rgba(255, 255, 255, 0.6);
  font-size: 1.1rem;
}

.content-area {
  width: 100%;
  display: flex;
  justify-content: center;
  min-height: 200px;
}

/* Loading Spinner */
.loading-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  color: rgba(255, 255, 255, 0.8);
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid rgba(255, 255, 255, 0.1);
  border-left-color: hsl(var(--color-primary-hsl));
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Error State */
.error-state {
  padding: 2rem;
  text-align: center;
  color: #fca5a5;
  border-color: rgba(252, 165, 165, 0.2);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.error-icon {
  font-size: 2rem;
}

.empty-state {
  color: rgba(255, 255, 255, 0.4);
  font-style: italic;
  margin-top: 2rem;
}
</style>
