<script setup>
defineProps({
  card: {
    type: Object,
    required: true
  },
  isFlipped: {
    type: Boolean,
    default: false
  }
})

defineEmits(['flip'])
</script>

<template>
  <div class="flashcard-wrapper" @click="$emit('flip')">
    <div class="flashcard" :class="{ 'is-flipped': isFlipped }">
      <div class="card-face front">
        <div class="content">
          <span class="text">{{ card.question }}</span>
        </div>
        <div class="hint">Tap to flip</div>
      </div>
      <div class="card-face back">
        <div class="content">
          <span class="label">Question</span>
          <span class="question-text">{{ card.question }}</span>
          <span class="label">Answer</span>
          <span class="answer-text">{{ card.answer }}</span>
          <div v-if="card.tip" class="tip-container">
            <span class="tip-icon">💡</span>
            <span class="tip-text">{{ card.tip }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.flashcard-wrapper {
  width: 100%;
  height: 220px;
  cursor: pointer;
  user-select: none;
  -webkit-user-select: none;
}

.flashcard {
  width: 100%;
  height: 100%;
  text-align: center;
  transition: all 0.3s ease-in-out;
  border-radius: 20px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  background: #ffffff;
  display: flex;
  flex-direction: column;
}

.flashcard-wrapper:hover .flashcard {
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2);
  transform: translateY(-8px);
}

.flashcard-wrapper:active .flashcard {
  transform: scale(0.98) translateY(-8px);
}

.card-face {
  width: 100%;
  height: 100%;
  border-radius: 20px;
  background: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 24px;
  overflow: hidden;
}

/* Front Face */
.front {
  background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
  border: 1px solid rgba(0, 0, 0, 0.05);
  display: flex;
}

.flashcard.is-flipped .front {
  display: none;
}

.front .text {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1a1a1a;
  line-height: 1.4;
}

.front .hint {
  position: absolute;
  bottom: 16px;
  font-size: 0.75rem;
  color: #9ca3af;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  font-weight: 500;
  opacity: 0;
  transform: translateY(4px);
  transition: all 0.3s ease;
}

.flashcard-wrapper:hover .front .hint {
  opacity: 1;
  transform: translateY(0);
}

/* Back Face */
.back {
  background: #ffffff;
  border: 1px solid rgba(0, 0, 0, 0.05);
  align-items: flex-start;
  text-align: left;
  display: none;
}

.flashcard.is-flipped .back {
  display: flex;
}

.back .content {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  overflow-y: auto;
  /* Custom scrollbar for webkit */
  scrollbar-width: thin;
  scrollbar-color: #e5e7eb transparent;
}

.back .content::-webkit-scrollbar {
  width: 4px;
}

.back .content::-webkit-scrollbar-thumb {
  background-color: #e5e7eb;
  border-radius: 4px;
}

.label {
  font-size: 0.7rem;
  text-transform: uppercase;
  color: #9ca3af;
  font-weight: 600;
  letter-spacing: 0.05em;
  margin-bottom: 4px;
}

.question-text {
  font-size: 0.95rem;
  color: #4b5563;
  margin-bottom: 12px;
  font-weight: 500;
}

.divider {
  height: 1px;
  background: #f3f4f6;
  width: 100%;
  margin: 8px 0 12px 0;
}

.answer-text {
  font-size: 1.1rem;
  color: #111827;
  font-weight: 600;
  line-height: 1.4;
}

.tip-container {
  padding-top: 12px;
  display: flex;
  gap: 8px;
  align-items: flex-start;
}

.tip-icon {
  font-size: 1rem;
}

.tip-text {
  font-size: 0.85rem;
  color: #6b7280;
  font-style: italic;
  line-height: 1.4;
}

@media (max-width: 900px) {
  .flashcard-wrapper {
    height: 220px;
  }
}
</style>
