<script setup>
import { ref, computed } from 'vue'

const query = ref('')

const concepts = [
  'Reactivity', 'Composables', 'Directives',
  'Vue Router', 'Pinia', 'Teleport',
]

// Computed property filters automatically on every input
const filtered = computed(() =>
  concepts.filter(k =>
    k.toLowerCase().includes(query.value.toLowerCase())
  )
)
</script>

<template>
  <div class="container">
    <!-- v-model: two-way binding to query -->
    <input
      v-model="query"
      placeholder="Search concept..."
      class="search-input"
    />

    <div class="count">
      {{ filtered.length }} / {{ concepts.length }} entries
    </div>

    <!-- v-for: renders filtered list reactively -->
    <ul class="list">
      <li
        v-for="concept in filtered"
        :key="concept"
        class="list-item"
      >
        {{ concept }}
      </li>
    </ul>

    <div v-if="filtered.length === 0" class="empty">
      No results
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
  width: auto;
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
