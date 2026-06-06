<script setup>
import { ref, computed } from 'vue'

const suche = ref('')

const konzepte = [
  'Reaktivität', 'Composables', 'Direktiven',
  'Vue Router', 'Pinia', 'Teleport',
]

// Computed-Property filtert automatisch bei jeder Eingabe
const gefilterteKonzepte = computed(() =>
  konzepte.filter(k =>
    k.toLowerCase().includes(suche.value.toLowerCase())
  )
)
</script>

<template>
  <div class="container">
    <!-- v-model: bidirektionale Bindung an suche -->
    <input
      v-model="suche"
      placeholder="Konzept suchen..."
      class="search-input"
    />

    <div class="count">
      {{ gefilterteKonzepte.length }} / {{ konzepte.length }} Einträge
    </div>

    <!-- v-for: rendert gefilterte Liste reaktiv -->
    <ul class="list">
      <li
        v-for="konzept in gefilterteKonzepte"
        :key="konzept"
        class="list-item"
      >
        {{ konzept }}
      </li>
    </ul>

    <div v-if="gefilterteKonzepte.length === 0" class="empty">
      Keine Treffer
    </div>
  </div>
</template>

<style scoped>
.container {
  padding: 1rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  font-family: sans-serif;
  max-width: 220px;
  background: white;
}
.search-input {
  width: 100%;
  padding: 0.4rem 0.6rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 0.9rem;
  box-sizing: border-box;
  margin-bottom: 0.5rem;
}
.search-input:focus {
  outline: none;
  border-color: #42b883;
}
.count {
  font-size: 0.72rem;
  color: #999;
  margin-bottom: 0.5rem;
}
.list {
  list-style: none;
  padding: 0;
  margin: 0;
}
.list-item {
  padding: 0.3rem 0.6rem;
  margin-bottom: 0.25rem;
  border-left: 3px solid #42b883;
  background: #f0faf5;
  border-radius: 2px;
  font-size: 0.88rem;
  color: #333;
}
.empty {
  color: #bbb;
  font-style: italic;
  font-size: 0.82rem;
  padding: 0.25rem 0;
}
</style>
