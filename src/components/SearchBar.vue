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
  <div class="search-wrapper">
    <div class="search-bar">
      <!-- Search Icon -->
      <svg class="search-icon" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <circle cx="11" cy="11" r="8"></circle>
        <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
      </svg>
      
      <input 
        v-model="city" 
        @keyup.enter="search"
        type="text" 
        placeholder="Search your City " 
        class="search-input"
      />
      
      <!-- Location Dropdown Trigger (Visual only) -->
      <!-- <div class="location-trigger">
        <span>Location</span>
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <polyline points="6 9 12 15 18 9"></polyline>
        </svg>
      </div> -->
    </div>
  </div>
</template>

<style scoped>
.search-wrapper {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.search-bar {
  display: flex;
  align-items: center;
  background: white;
  border-radius: 4px; /* Slightly rounded corners, almost rectangular */
  padding: 0.5rem 1rem;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  height: 56px;
}

.search-icon {
  color: #64748b; /* Slate-500 */
  margin-right: 0.75rem;
}

.search-input {
  flex: 1;
  border: none;
  border-radius: 0; /* Input inside has no radius */
  outline: none;
  font-size: 1rem;
  color: #334155;
  background: transparent;
  padding: 0;
}

.search-input::placeholder {
  color: #94a3b8;
}

.location-trigger {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding-left: 1rem;
  border-left: 1px solid #e2e8f0;
  margin-left: 0.5rem;
  color: #64748b;
  font-size: 0.9rem;
  cursor: pointer;
  white-space: nowrap;
}

.location-trigger:hover {
  color: #334155;
}

@media (max-width: 600px) {
  .location-trigger {
    display: none; /* Hide on small screens if needed */
  }
}
</style>
