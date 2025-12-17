<script setup>
import { computed } from 'vue'

const props = defineProps({
  weather: {
    type: Object,
    required: true
  }
})

// Weather code mapping
const weatherCondition = computed(() => {
  const code = props.weather.weathercode
  
  if (code === 0) return { label: 'Sunny', icon: '☀️' }
  if (code >= 1 && code <= 3) return { label: 'Partly Cloudy', icon: '⛅' }
  if (code === 45 || code === 48) return { label: 'Foggy', icon: '🌫️' }
  if (code >= 51 && code <= 57) return { label: 'Drizzle', icon: 'Vm' }
  if (code >= 61 && code <= 67) return { label: 'Rainy', icon: 'Vm' }
  if (code >= 71 && code <= 77) return { label: 'Snowy', icon: '❄️' }
  if (code >= 80 && code <= 82) return { label: 'Showers', icon: '🌦️' }
  if (code >= 95 && code <= 99) return { label: 'Thunderstorm', icon: '⛈️' }
  
  return { label: 'Unknown', icon: '❓' }
})
</script>

<template>
  <div class="weather-card">
    <div class="card-header">
      <h3 class="section-label">RECENT LOCATIONS</h3>
    </div>
    
    <div class="card-content glass-dark">
      <div class="location-info">
        <h2 class="city-name">{{ weather.name }}</h2>
        <p class="country-name">{{ weather.country || 'Cote D\'Ivoire' }}</p> <!-- Fallback as API might not provide country always -->
      </div>
      
      <div class="weather-info">
        <div class="main-weather">
          <span class="weather-icon">{{ weatherCondition.icon }}</span>
          <span class="temperature">{{ Math.round(weather.temperature) }}<span class="degree">°C</span></span>
        </div>
        <p class="real-feel">RealFeel® {{ Math.round(weather.temperature + 2) }}°</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.weather-card {
  width: 100%;
  max-width: 340px; /* Card size from image */
  text-align: left;
  animation: fadeIn 0.5s ease;
}

.section-label {
  font-size: 0.75rem;
  font-weight: 700;
  color: rgba(255, 255, 255, 0.9);
  margin-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.glass-dark {
  background: rgba(30, 30, 30, 0.6); /* Darker translucent background */
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border-radius: 12px;
  padding: 1.25rem;
  color: white;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: transform 0.2s;
  cursor: pointer;
}

.glass-dark:hover {
  transform: translateY(-2px);
  background: rgba(30, 30, 30, 0.7);
}

.location-info {
  margin-bottom: 1.5rem;
}

.city-name {
  font-size: 1.5rem;
  font-weight: 400; /* Regular weight */
  margin: 0;
  line-height: 1.2;
}

.country-name {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.7);
  margin-top: 0.25rem;
}

/* Layout for bottom section */
.weather-info {
  margin-top: auto;
}

.main-weather {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 0.25rem;
}

.weather-icon {
  font-size: 2.5rem; /* Large icon */
}

.temperature {
  font-size: 2.5rem;
  font-weight: 300; /* Thin/Light */
  line-height: 1;
}

.degree {
  font-size: 1.5rem;
  vertical-align: top;
  margin-left: 2px;
}

.real-feel {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.7);
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
