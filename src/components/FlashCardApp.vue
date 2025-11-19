<script setup>
import { ref, computed } from 'vue'
import AppNavbar from './AppNavbar.vue'
import AppSidebar from './AppSidebar.vue'
import FlashCard from './FlashCard.vue'

// Dynamic import of all json files in ../flashcards
const subjectsFiles = import.meta.glob('../flashcards/*.json', { eager: true })
const subjects = {}

for (const path in subjectsFiles) {
  // Extract filename without extension as subject name
  const subjectName = path.split('/').pop().replace('.json', '')
  subjects[subjectName] = subjectsFiles[path].default || subjectsFiles[path]
}

const subjectNames = Object.keys(subjects)
const currentSubject = ref(subjectNames[0] || '')

const categories = computed(() => {
  return currentSubject.value ? Object.keys(subjects[currentSubject.value]) : []
})

const cardsByCategory = computed(() => {
  return currentSubject.value ? subjects[currentSubject.value] : {}
})

const flippedCards = ref({})
const isSidebarOpen = ref(false)

// Watch for subject changes to reset flipped cards
import { watch } from 'vue'

watch(currentSubject, (newSubject) => {
  if (newSubject) {
    flippedCards.value = {}
    categories.value.forEach(cat => {
      flippedCards.value[cat] = cardsByCategory.value[cat].map(() => false)
    })
  }
}, { immediate: true })

function changeSubject(subject) {
  currentSubject.value = subject
  isSidebarOpen.value = false
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

function flipCard(cat, idx) {
  flippedCards.value[cat][idx] = !flippedCards.value[cat][idx]
}

function toggleSidebar() {
  isSidebarOpen.value = !isSidebarOpen.value
}

function scrollToCategory(cat) {
  const element = document.getElementById('cat-' + cat)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    isSidebarOpen.value = false
  }
}
</script>

<template>
  <div class="app-wrapper">
    <AppNavbar :subjects="subjectNames" :current-subject="currentSubject" @change-subject="changeSubject" />

    <AppSidebar :is-open="isSidebarOpen" :categories="categories" @toggle="toggleSidebar"
      @select-category="scrollToCategory" />

    <div class="container" :class="{ 'sidebar-open': isSidebarOpen }">
      <div v-for="cat in categories" :key="cat" :id="'cat-' + cat" class="category-block">
        <h2 class="category-title">{{ cat }}</h2>
        <div class="flashcard-list">
          <FlashCard v-for="(card, idx) in cardsByCategory[cat]" :key="card.id || idx" :card="card"
            :is-flipped="flippedCards[cat][idx]" @flip="flipCard(cat, idx)" />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  min-height: 100vh;
  background: #0f0f11;
  /* Deep dark background */
  background: radial-gradient(circle at top left, #1a1a2e 0%, #0f0f11 100%);
}

.container {
  min-height: 100vh;
  margin: 0 auto;
  padding-top: 100px;
  /* Space for navbar + extra */
  padding-bottom: 60px;
  font-family: 'Inter', sans-serif;
  transition: transform 0.5s cubic-bezier(0.19, 1, 0.22, 1);
  max-width: 1200px;
  padding-left: 24px;
  padding-right: 24px;
}

.category-block {
  margin-bottom: 60px;
}

.category-title {
  font-size: 1.75rem;
  font-weight: 700;
  color: #fff;
  margin-bottom: 24px;
  letter-spacing: -0.02em;
  padding-left: 8px;
  border-left: 4px solid #6366f1;
  line-height: 1;
}

.flashcard-list {
  display: flex;
  flex-wrap: wrap;
  gap: 32px;
  justify-content: flex-start;
  /* Align left for grid-like feel */
  align-items: stretch;
  user-select: none;
}

@media (max-width: 900px) {
  .flashcard-list {
    gap: 20px;
    justify-content: center;
  }

  .container {
    padding-top: 90px;
    padding-left: 16px;
    padding-right: 16px;
  }

  .category-title {
    font-size: 1.5rem;
    margin-bottom: 20px;
  }
}

/* Optional: Push content when sidebar is open on large screens */
@media (min-width: 1200px) {
  .container.sidebar-open {
    transform: translateX(160px);
  }
}
</style>
