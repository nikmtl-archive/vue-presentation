<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const multiplikator = ref(2)

// Wird automatisch neu berechnet, wenn count oder multiplikator sich ändern
const ergebnis = computed(() => count.value * multiplikator.value)
</script>

<template>
  <div class="container">
    <div class="row">
      <button @click="count++" class="btn">+1</button>
      <span class="counter-val">Zähler: {{ count }}</span>
      <button @click="count--" class="btn btn-outline">−1</button>
    </div>

    <div class="row">
      <label class="label">Multiplikator:</label>
      <input
        v-model.number="multiplikator"
        type="number"
        min="1"
        max="20"
        class="num-input"
      />
    </div>

    <div class="result">
      <span class="formula">{{ count }} × {{ multiplikator }} =</span>
      <span class="answer">{{ ergebnis }}</span>
    </div>

    <div class="hint">computed() – automatisch aktualisiert</div>
  </div>
</template>

<style scoped>
.container {
  padding: 1.25rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  font-family: sans-serif;
  max-width: 260px;
  background: white;
}
.row {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.75rem;
}
.btn {
  background: #42b883;
  color: white;
  border: none;
  padding: 0.35rem 0.7rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
}
.btn-outline {
  background: transparent;
  color: #42b883;
  border: 2px solid #42b883;
}
.btn:hover { opacity: 0.85; }
.counter-val {
  font-size: 0.95rem;
  font-weight: 600;
  color: #333;
}
.label {
  font-size: 0.9rem;
  color: #555;
}
.num-input {
  width: 56px;
  padding: 0.2rem 0.4rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 1rem;
  text-align: center;
}
.result {
  background: #f0faf5;
  padding: 0.65rem 0.85rem;
  border-radius: 4px;
  margin-bottom: 0.5rem;
  font-size: 1.15rem;
}
.formula { color: #666; margin-right: 0.3rem; }
.answer { color: #42b883; font-weight: bold; font-size: 1.3rem; }
.hint {
  font-size: 0.72rem;
  color: #aaa;
  text-align: center;
}
</style>
