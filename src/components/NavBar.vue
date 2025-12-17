<script setup>
import { ref } from 'vue'

const menuOpen = ref(false)
const emit = defineEmits(['open-settings'])
</script>

<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="brand">
        <!-- Sun Icon -->
        <svg class="brand-icon" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="12" cy="12" r="6" fill="#f97316"/>
          <path d="M12 2V4" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M12 20V22" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M22 12H20" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M4 12H2" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M19.071 4.929L17.657 6.343" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M6.343 17.657L4.929 19.071" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M19.071 19.071L17.657 17.657" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
          <path d="M6.343 6.343L4.929 4.929" stroke="#f97316" stroke-width="2" stroke-linecap="round"/>
        </svg>
        <span class="brand-name">WeatherDash</span>
      </div>

      <div class="nav-links desktop-only">
        <!-- <a href="#" class="nav-link active">For Business</a>
        <a href="#" class="nav-link">Warnings</a>
        <a href="#" class="nav-link">Data Suite</a>
        <a href="#" class="nav-link">Forensics</a>
        <a href="#" class="nav-link">Advertising</a>
        <a href="#" class="nav-link">Superior Accuracy™</a> -->
      </div>

      <div class="right-actions">
        <!-- Settings Icon -->
        <button class="settings-btn" @click="$emit('open-settings')">
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12.22 2h-.44a2 2 0 0 0-2 2v.18a2 2 0 0 1-1 1.73l-.43.25a2 2 0 0 1-2 0l-.15-.08a2 2 0 0 0-2.73.73l-.22.38a2 2 0 0 0 .73 2.73l.15.1a2 2 0 0 1 1 1.72v.51a2 2 0 0 1-1 1.74l-.15.09a2 2 0 0 0-.73 2.73l.22.38a2 2 0 0 0 2.73.73l.15-.08a2 2 0 0 1 2 0l.43.25a2 2 0 0 1 1 1.73V20a2 2 0 0 0 2 2h.44a2 2 0 0 0 2-2v-.18a2 2 0 0 1 1-1.73l.43-.25a2 2 0 0 1 2 0l.15.08a2 2 0 0 0 2.73-.73l.22-.38a2 2 0 0 0-.73-2.73l-.15-.1a2 2 0 0 1-1-1.72v-.51a2 2 0 0 1 1-1.74l.15-.09a2 2 0 0 0 .73-2.73l-.22-.38a2 2 0 0 0-2.73-.73l-.15.08a2 2 0 0 1-2 0l-.43-.25a2 2 0 0 1-1-1.73V4a2 2 0 0 0-2-2z"></path>
            <circle cx="12" cy="12" r="3"></circle>
          </svg>
        </button>

        <div class="mobile-toggle" @click="menuOpen = !menuOpen">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="3" y1="12" x2="21" y2="12"></line>
            <line x1="3" y1="6" x2="21" y2="6"></line>
            <line x1="3" y1="18" x2="21" y2="18"></line>
          </svg>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  width: 100%;
  background: rgba(0, 0, 0, 0.7);
  backdrop-filter: blur(5px);
  padding: 0.5rem 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1); 
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 48px;
}

.brand {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

.brand-icon {
  width: 28px;
  height: 28px;
}

.brand-name {
  font-size: 1.25rem;
  font-weight: 700;
  color: white;
  letter-spacing: -0.5px;
}

.nav-links {
  display: flex;
  gap: 1.5rem;
  align-items: center;
}

.nav-link {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  transition: color 0.2s;
  text-transform: uppercase;
  font-size: 0.75rem; /* Smaller font for top bar links */
  letter-spacing: 0.5px;
}

.nav-link:hover, .nav-link.active {
  color: white;
}

.right-actions {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.settings-btn {
  background: none;
  border: none;
  color: rgba(255, 255, 255, 0.7);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5rem;
  border-radius: 50%;
  transition: all 0.2s;
}

.settings-btn:hover {
  color: white;
  background: rgba(255, 255, 255, 0.1);
}

.mobile-toggle {
  display: none;
  cursor: pointer;
  color: white;
}

@media (max-width: 900px) {
  .desktop-only {
    display: none;
  }
  
  .mobile-toggle {
    display: block;
  }
}
</style>
