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
  <!-- Sidebar -->
  <div class="sidebar" :class="{ 'open': isOpen }">
    <div class="sidebar-header">
      <button class="close-btn" @click="$emit('toggle')">✕</button>
    </div>
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

.sidebar-header {
  padding: 20px;
  display: flex;
  justify-content: flex-end;
}

.close-btn {
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.6);
  font-size: 1.5rem;
  cursor: pointer;
  padding: 8px;
  border-radius: 8px;
  transition: all 0.2s ease;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.close-btn:hover {
  background: rgba(255, 255, 255, 0.1);
  color: #fff;
}

.sidebar-content {
  padding: 20px 32px 40px;
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
