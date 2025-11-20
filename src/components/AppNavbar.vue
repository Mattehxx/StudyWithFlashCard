<script setup>
import { ref } from 'vue'

defineProps({
  subjects: {
    type: Array,
    required: true
  },
  currentSubject: {
    type: String,
    required: true
  },
  isOpen: {
    type: Boolean,
    required: true
  }
})

defineEmits(['change-subject', 'toggle-sidebar'])

const isDropdownOpen = ref(false)
</script>

<template>
  <nav class="navbar">
    <div class="nav-content">
      <div class="nav-left">
        <button class="sidebar-toggle" @click="$emit('toggle-sidebar')" :class="{ 'open': isOpen }">
          <span v-if="!isOpen">☰</span>
          <span v-else>✕</span>
        </button>
      </div>

      <div class="nav-center">
        <div class="nav-brand">StudyCards</div>
      </div>

      <div class="nav-right">
        <div class="dropdown-wrapper" @mouseenter="isDropdownOpen = true" @mouseleave="isDropdownOpen = false">
          <button class="dropdown-trigger" :class="{ active: isDropdownOpen }">
            Materie <span class="arrow">▼</span>
          </button>

          <transition name="fade">
            <div v-if="isDropdownOpen" class="dropdown-menu">
              <button v-for="subject in subjects" :key="subject" class="dropdown-item"
                :class="{ active: currentSubject === subject }"
                @click="$emit('change-subject', subject); isDropdownOpen = false">
                {{ subject }}
              </button>
            </div>
          </transition>
        </div>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 70px;
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  z-index: 900;
  display: flex;
  justify-content: center;
  transition: all 0.3s ease;
}

.nav-content {
  width: 100%;
  max-width: 1600px;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 0 24px;
}

.nav-left {
  display: flex;
  justify-content: flex-start;
}

.nav-center {
  display: flex;
  justify-content: center;
}

.nav-right {
  display: flex;
  justify-content: flex-end;
}

.sidebar-toggle {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  border-radius: 12px;
  width: 40px;
  height: 40px;
  font-size: 1.2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.sidebar-toggle:hover {
  background: rgba(255, 255, 255, 0.2);
}

.sidebar-toggle.open {
  background: #fff;
  color: #000;
}

.nav-brand {
  color: #fff;
  font-weight: 800;
  font-size: 1.4rem;
  letter-spacing: -0.02em;
  background: linear-gradient(135deg, #fff 0%, #a5b4fc 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.dropdown-wrapper {
  position: relative;
}

.dropdown-trigger {
  background: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.05);
  color: rgba(255, 255, 255, 0.8);
  padding: 8px 16px;
  border-radius: 12px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: all 0.3s ease;
}

.dropdown-trigger:hover,
.dropdown-trigger.active {
  background: rgba(255, 255, 255, 0.1);
  color: #fff;
  border-color: rgba(255, 255, 255, 0.1);
}

.arrow {
  font-size: 0.7rem;
  transition: transform 0.3s ease;
}

.dropdown-trigger.active .arrow {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  right: 0;
  margin-top: 8px;
  background: rgba(15, 15, 15, 0.95);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 8px;
  min-width: 180px;
  display: flex;
  flex-direction: column;
  gap: 4px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
}

.dropdown-item {
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.6);
  padding: 10px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  text-align: left;
  text-transform: capitalize;
  transition: all 0.2s ease;
  width: 100%;
}

.dropdown-item:hover {
  background: rgba(255, 255, 255, 0.05);
  color: #fff;
}

.dropdown-item.active {
  background: #fff;
  color: #000;
  font-weight: 600;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>
