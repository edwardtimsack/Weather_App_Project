<template>
  <div class="weather-card">
    <h2>{{ city }}</h2>
    <div class="weather-icon">{{ getWeatherIcon(data.weather_code) }}</div>
    <div class="temperature">{{ Math.round(data.temperature_2m) }}°C</div>
    <p class="condition">{{ getWeatherDescription(data.weather_code) }}</p>

    <div class="weather-details">
      <div class="detail">
        <span class="label">Wind Speed</span>
        <span class="value">{{ data.wind_speed_10m }} km/h</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true
    },
    city: {
      type: String,
      required: true
    }
  },
  methods: {
    getWeatherIcon(code) {
      if (code === 0) return '☀️'
      if (code === 1 || code === 2) return '🌤️'
      if (code === 3) return '☁️'
      if (code === 45 || code === 48) return '🌫️'
      if (code === 51 || code === 53 || code === 55) return '🌦️'
      if (code === 61 || code === 63 || code === 65) return '🌧️'
      if (code === 71 || code === 73 || code === 75 || code === 77) return '🌨️'
      if (code === 80 || code === 81 || code === 82) return '⛈️'
      if (code === 85 || code === 86) return '🌨️'
      return '🌤️'
    },
    getWeatherDescription(code) {
      const descriptions = {
        0: 'Clear sky',
        1: 'Mainly clear',
        2: 'Partly cloudy',
        3: 'Overcast',
        45: 'Foggy',
        48: 'Foggy',
        51: 'Light drizzle',
        53: 'Moderate drizzle',
        55: 'Dense drizzle',
        61: 'Slight rain',
        63: 'Moderate rain',
        65: 'Heavy rain',
        71: 'Slight snow',
        73: 'Moderate snow',
        75: 'Heavy snow',
        77: 'Snow grains',
        80: 'Slight rain showers',
        81: 'Moderate rain showers',
        82: 'Violent rain showers',
        85: 'Slight snow showers',
        86: 'Heavy snow showers'
      }
      return descriptions[code] || 'Unknown'
    }
  }
}
</script>

<style scoped>
.weather-card {
  animation: slideIn 0.5s ease-out;
  padding: 30px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 15px;
  color: white;
}

h2 {
  font-size: 24px;
  margin-bottom: 20px;
  font-weight: 600;
}

.weather-icon {
  font-size: 80px;
  margin: 20px 0;
}

.temperature {
  font-size: 48px;
  font-weight: 700;
  margin: 15px 0;
}

.condition {
  font-size: 18px;
  margin-bottom: 25px;
  opacity: 0.9;
}

.weather-details {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 10px;
  padding: 20px;
  margin-top: 20px;
}

.detail {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
}

.label {
  opacity: 0.9;
  font-size: 14px;
}

.value {
  font-size: 18px;
  font-weight: 600;
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 600px) {
  .weather-card {
    padding: 20px;
  }

  .temperature {
    font-size: 36px;
  }

  .weather-icon {
    font-size: 60px;
  }
}
</style>