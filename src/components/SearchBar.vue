<script setup>
import { ref } from 'vue'

const city = ref('')
const emit = defineEmits(['search-city'])

const search = () => {
  if (city.value.trim()) {
    emit('search-city', city.value.trim())
    city.value = '' // Optional: clear after search, or keep it. Let's keep it clear for now.
  }
}
</script>

<template>
  <div class="search-container glass-panel">
    <input 
      v-model="city" 
      @keyup.enter="search"
      type="text" 
      placeholder="Enter city name..." 
      class="search-input"
    />
    <button @click="search" class="btn-primary">
      Search
    </button>
  </div>
</template>

<style scoped>
.search-container {
  display: flex;
  gap: 1rem;
  padding: 1rem;
  width: 100%;
  max-width: 500px;
}

.search-input {
  flex: 1;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  padding: 0.75rem 1rem;
  color: white;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s;
}

.search-input:focus {
  border-color: hsl(var(--color-primary-hsl));
  background: rgba(255, 255, 255, 0.1);
}

.search-input::placeholder {
  color: rgba(255, 255, 255, 0.5);
}

@media (max-width: 600px) {
  .search-container {
    flex-direction: column;
  }
  
  .btn-primary {
    width: 100%;
  }
}
</style>
