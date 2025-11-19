<script setup>
defineProps({
  subjects: {
    type: Array,
    required: true
  },
  currentSubject: {
    type: String,
    required: true
  }
})

defineEmits(['change-subject'])
</script>

<template>
  <nav class="navbar">
    <div class="nav-content">
      <div class="nav-brand">StudyCards</div>
      <div class="nav-links">
        <button v-for="subject in subjects" :key="subject" class="nav-item"
          :class="{ active: currentSubject === subject }" @click="$emit('change-subject', subject)">
          {{ subject }}
        </button>
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
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  display: flex;
  justify-content: center;
  transition: all 0.3s ease;
}

.nav-content {
  width: 100%;
  max-width: 1200px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
  padding-left: 80px;
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

.nav-links {
  display: flex;
  gap: 8px;
  background: rgba(0, 0, 0, 0.2);
  padding: 4px;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.nav-item {
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.6);
  padding: 8px 16px;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  text-transform: capitalize;
  position: relative;
}

.nav-item:hover {
  color: #fff;
  background: rgba(255, 255, 255, 0.05);
}

.nav-item.active {
  color: #000;
  background: #fff;
  font-weight: 600;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}
</style>
