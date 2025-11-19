<script setup>
defineProps({
  isOpen: {
    type: Boolean,
    required: true
  },
  categories: {
    type: Array,
    required: true
  }
})

defineEmits(['toggle', 'select-category'])
</script>

<template>
  <!-- Toggle Button -->
  <button class="sidebar-toggle" @click="$emit('toggle')" :class="{ 'open': isOpen }">
    <span v-if="!isOpen">☰</span>
    <span v-else>✕</span>
  </button>

  <!-- Sidebar -->
  <div class="sidebar" :class="{ 'open': isOpen }">
    <div class="sidebar-content">
      <h3>Categorie</h3>
      <ul>
        <li v-for="cat in categories" :key="cat" @click="$emit('select-category', cat)">
          {{ cat }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.sidebar-toggle {
  position: fixed;
  top: 12px;
  left: 20px;
  z-index: 1001;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  border-radius: 12px;
  width: 46px;
  height: 46px;
  font-size: 1.2rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.sidebar-toggle:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: scale(1.05);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
}

.sidebar-toggle.open {
  background: #fff;
  color: #000;
}

.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 320px;
  background: rgba(15, 15, 15, 0.95);
  backdrop-filter: blur(24px);
  -webkit-backdrop-filter: blur(24px);
  z-index: 1000;
  transform: translateX(-100%);
  transition: transform 0.5s cubic-bezier(0.19, 1, 0.22, 1);
  box-shadow: 20px 0 50px rgba(0, 0, 0, 0.3);
  border-right: 1px solid rgba(255, 255, 255, 0.05);
  overflow-y: auto;
}

.sidebar.open {
  transform: translateX(0);
}

.sidebar-content {
  padding: 100px 32px 40px;
}

.sidebar-content h3 {
  color: rgba(255, 255, 255, 0.4);
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  margin-bottom: 24px;
  font-weight: 700;
}

.sidebar-content ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.sidebar-content li {
  color: rgba(255, 255, 255, 0.8);
  padding: 16px 20px;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.2s ease;
  font-weight: 500;
  font-size: 1rem;
  border: 1px solid transparent;
}

.sidebar-content li:hover {
  background: rgba(255, 255, 255, 0.05);
  color: #fff;
  border-color: rgba(255, 255, 255, 0.05);
  transform: translateX(4px);
}
</style>
