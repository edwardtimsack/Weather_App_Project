<template>
  <div class="search-bar">
    <input
      v-model="searchInput"
      type="text"
      placeholder="Enter city name..."
      @keyup.enter="search"
      class="search-input"
    />
    <button @click="search" class="search-button">Search</button>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  emits: ['search'],
  setup(props, { emit }) {
    const searchInput = ref('')

    const search = () => {
      if (searchInput.value.trim()) {
        emit('search', searchInput.value.trim())
        searchInput.value = ''
      }
    }

    return {
      searchInput,
      search
    }
  }
}
</script>

<style scoped>
.search-bar {
  display: flex;
  gap: 10px;
  margin-bottom: 30px;
}

.search-input {
  flex: 1;
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 16px;
  transition: border-color 0.3s;
}

.search-input:focus {
  outline: none;
  border-color: #667eea;
}

.search-button {
  padding: 12px 30px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  font-weight: 600;
  transition: transform 0.2s, box-shadow 0.2s;
}

.search-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
}

.search-button:active {
  transform: translateY(0);
}

@media (max-width: 600px) {
  .search-bar {
    flex-direction: column;
    gap: 12px;
  }

  .search-button {
    width: 100%;
  }
}
</style>
