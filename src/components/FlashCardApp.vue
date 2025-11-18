<template>
  <div class="container">
    <div v-for="cat in categories" :key="cat" class="category-block">
      <h2 class="category-title">{{ cat }}</h2>
      <div class="flashcard-list">
        <div v-for="(card, idx) in cardsByCategory[cat]" :key="card.id" class="flashcard" @click="flipCard(cat, idx)">
          <div v-if="!flippedCards[cat][idx]" class="front" key="question">
            <span>{{ card.question }}</span>
          </div>
          <div v-else class="back" key="answer">
            <span class="question">{{ card.question }}</span>
            <span class="answer">{{ card.answer }}</span>
            <span v-if="card.tip" class="tip">{{ card.tip }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import cardsJson from '../flashcards.json'

const categories = Object.keys(cardsJson)
const cardsByCategory = cardsJson

const flippedCards = ref({})
categories.forEach(cat => {
  flippedCards.value[cat] = cardsByCategory[cat].map(() => false)
})

function flipCard(cat, idx) {
  flippedCards.value[cat][idx] = !flippedCards.value[cat][idx]
}
</script>

<style scoped>
.container {
  min-height: 100vh;
  margin: 2rem auto;
  font-family: 'Inter', Arial, sans-serif;
}
.category-block {
  margin-bottom: 40px;
}
.category-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #fff;
  margin-bottom: 18px;
  letter-spacing: 0.02em;
}
.container {
  min-height: 100vh;
  margin: 2rem auto;
  font-family: 'Inter', Arial, sans-serif;
}

.flashcard-list {
  display: flex;
  flex-wrap: wrap;
  gap: 32px;
  justify-content: center;
  align-items: stretch;
  user-select: none;
}

.flashcard {
  width: 260px;
  min-height: 180px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 12px 16px;
  box-shadow: 0 2px 16px rgba(0, 0, 0, 0.08);
  border: 1px solid #e0e0e0;
  border-radius: 14px;
  background: #fff;
}

.flashcard .front,
.flashcard .back {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 12px;
  font-size: 1.18rem;
}

.flashcard .front {
  color: #222;
  font-weight: 500;
  letter-spacing: 0.01em;
}

.flashcard .back {
  color: #222;
  font-weight: 600;
  letter-spacing: 0.01em;
}

.flashcard .back .question {
  font-size: 1rem;
  color: #222;
  font-weight: 500;
}

.flashcard .back .answer {
  text-decoration: underline;
}

.flashcard .back .tip {
  font-size: 0.9rem;
  color: #555;
  font-style: italic;
  font-weight: 600;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s cubic-bezier(.4, 2, .3, 1);
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 900px) {
  .flashcard-list {
    gap: 18px;
  }

  .container {
    max-width: 98vw;
    padding: 18px 4vw 18px 4vw;
  }

  .flashcard {
    width: 98vw;
    max-width: 260px;
    height: 140px;
  }
}
</style>
