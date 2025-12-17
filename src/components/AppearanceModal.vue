<script setup>
defineProps({
  isOpen: Boolean,
  currentTheme: String
})

const emit = defineEmits(['close', 'set-theme'])
</script>

<template>
  <div v-if="isOpen" class="modal-overlay" @click.self="$emit('close')">
    <div class="modal-content glass-panel">
      <div class="modal-header">
        <h2>Appearance</h2>
        <button class="close-btn" @click="$emit('close')">&times;</button>
      </div>
      
      <div class="theme-options">
        <button 
          class="theme-btn" 
          :class="{ active: currentTheme === 'light' }"
          @click="$emit('set-theme', 'light')"
        >
          <div class="preview light"></div>
          <span>Light</span>
        </button>
        
        <button 
          class="theme-btn" 
          :class="{ active: currentTheme === 'dark' }"
          @click="$emit('set-theme', 'dark')"
        >
          <div class="preview dark"></div>
          <span>Dark</span>
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  backdrop-filter: blur(4px);
}

.modal-content {
  background: #1e1e1e;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 16px;
  padding: 1.5rem;
  width: 90%;
  max-width: 400px;
  color: white;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.modal-header h2 {
  margin: 0;
  font-size: 1.5rem;
}

.close-btn {
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.6);
  font-size: 2rem;
  cursor: pointer;
  padding: 0;
  line-height: 1;
}

.close-btn:hover {
  color: white;
}

.theme-options {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.theme-btn {
  background: rgba(255, 255, 255, 0.05);
  border: 2px solid transparent;
  border-radius: 12px;
  padding: 1rem;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  transition: all 0.2s;
}

.theme-btn:hover {
  background: rgba(255, 255, 255, 0.1);
}

.theme-btn.active {
  border-color: #f97316; /* Brand orange */
  background: rgba(249, 115, 22, 0.1);
}

.theme-btn span {
  color: white;
  font-weight: 500;
}

.preview {
  width: 100%;
  height: 60px;
  border-radius: 8px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.preview.light {
  background: linear-gradient(to bottom, #e0f2fe, #fff);
}

.preview.dark {
  background: linear-gradient(to bottom, #1e1e2e, #0f0f16);
}
</style>
