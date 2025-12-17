<script setup>
import { ref, onMounted } from 'vue'
import SearchBar from './components/SearchBar.vue'
import WeatherCard from './components/WeatherCard.vue'
import NavBar from './components/NavBar.vue'
import AppearanceModal from './components/AppearanceModal.vue'
import Footer from './components/Footer.vue'

const weatherData = ref(null)
const loading = ref(false)
const error = ref(null)
const showSettings = ref(false)
const currentTheme = ref('dark')

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
    console.log('API Response:', data)
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

const setTheme = (theme) => {
  currentTheme.value = theme
  document.documentElement.setAttribute('data-theme', theme)
}

onMounted(() => {
  handleSearch('Monrovia')
  // Set default theme
  document.documentElement.setAttribute('data-theme', 'dark')
})
</script>

<template>
  <div class="app-container">
    <NavBar @open-settings="showSettings = true" />
    
    <AppearanceModal 
      :is-open="showSettings" 
      :current-theme="currentTheme"
      @close="showSettings = false"
      @set-theme="setTheme"
    />
    
    <main class="main-content">
      <!-- Search Section -->
      <section class="search-section">
        <SearchBar @search-city="handleSearch" />
      </section>

      <!-- Content Area -->
      <div class="content-area">
        <div v-if="loading" class="loading-state">
          <div class="spinner"></div>
        </div>

        <div v-else-if="error" class="error-state">
          <span class="error-text">{{ error }}</span>
        </div>

        <div v-else-if="weatherData" class="cards-container">
          <!-- We could have multiple cards here, but for now just the main one -->
          <WeatherCard :weather="weatherData" />
        </div>
        
        <!-- Empty state is hidden or just empty spacing in the new design -->
      </div>
    </main>
    
    <Footer />
  </div>
</template>

<style scoped>
.app-container {
  width: 100%;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.main-content {
  flex: 1;
  width: 100%;
  max-width: 1200px; /* Aligned with standard desktop widths */
  margin: 0 auto;
  padding: 4rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 3rem;
}

.search-section {
  width: 100%;
  display: flex;
  justify-content: center;
  margin-top: 2rem; /* Push down a bit from navbar */
}

.content-area {
  display: flex;
  flex-direction: column;
  align-items: flex-start; /* Align contents to left like the image (Recent Locations) */
  padding-left: 10%; /* Roughly position it like the screenshot */
}

.cards-container {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

/* Loading Spinner */
.loading-state {
  width: 100%;
  display: flex;
  justify-content: center;
  padding: 2rem;
}

.spinner {
  width: 40px;
  height: 40px;
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-left-color: white;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Error State */
.error-state {
  width: 100%;
  text-align: center;
  padding: 1rem;
  background: rgba(220, 38, 38, 0.8);
  border-radius: 8px;
  color: white;
}

@media (max-width: 768px) {
  .main-content {
    padding: 2rem 1rem;
    align-items: center;
  }
  
  .content-area {
    padding-left: 0;
    align-items: center;
    width: 100%;
  }
  
  .cards-container {
    justify-content: center;
  }
}
</style>
