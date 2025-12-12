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
  <div class="weather-card glass-panel">
    <div class="card-header">
      <h2 class="city-name">{{ weather.name }}</h2>
      <span class="weather-icon">{{ weatherCondition.icon }}</span>
    </div>
    
    <div class="card-body">
      <div class="temp-container">
        <span class="temperature">{{ Math.round(weather.temperature) }}°C</span>
        <span class="condition">{{ weatherCondition.label }}</span>
      </div>
      
      <div class="details-grid">
        <div class="detail-item">
          <span class="label">Wind Speed</span>
          <span class="value">{{ weather.windspeed }} km/h</span>
        </div>
        <!-- Expandable for future props like humidity -->
      </div>
    </div>
  </div>
</template>

<style scoped>
.weather-card {
  padding: 2rem;
  width: 100%;
  max-width: 400px;
  animation: slideUp 0.5s ease-out;
  color: white;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.city-name {
  font-size: 2rem;
  font-weight: 700;
  margin: 0;
}

.weather-icon {
  font-size: 3rem;
}

.temp-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 2rem;
}

.temperature {
  font-size: 4rem;
  font-weight: 800;
  line-height: 1;
  background: linear-gradient(to bottom, #fff, #a5b4fc);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.condition {
  font-size: 1.25rem;
  color: rgba(255, 255, 255, 0.8);
  margin-top: 0.5rem;
}

.details-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.detail-item {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  text-align: center;
}

.label {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.6);
}

.value {
  font-size: 1.125rem;
  font-weight: 600;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
