<script setup>
import { ref } from 'vue'

// Inline-Composable – gleiche Logik wie useFetch.js, hier eingebettet
function useFetch(url) {
  const daten = ref(null)
  const laedt = ref(false)
  const fehler = ref(null)

  async function abrufen() {
    laedt.value = true
    fehler.value = null
    daten.value = null
    try {
      const antwort = await fetch(url)
      if (!antwort.ok) throw new Error(`HTTP ${antwort.status}`)
      daten.value = await antwort.json()
    } catch (e) {
      fehler.value = e.message
    } finally {
      laedt.value = false
    }
  }

  abrufen() // Automatisch beim Einbinden ausführen
  return { daten, laedt, fehler, erneut: abrufen }
}

const { daten, laedt, fehler, erneut } = useFetch(
  'https://jsonplaceholder.typicode.com/todos/1'
)
</script>

<template>
  <div class="container">
    <div class="url-label">GET /todos/1</div>

    <div v-if="laedt" class="status loading">Lädt...</div>
    <div v-else-if="fehler" class="status error">Fehler: {{ fehler }}</div>
    <div v-else-if="daten">
      <div class="resp-label">Antwort:</div>
      <pre class="json">{{ JSON.stringify(daten, null, 2) }}</pre>
    </div>

    <button
      @click="erneut"
      :disabled="laedt"
      class="btn"
    >
      {{ laedt ? 'Lädt...' : 'Erneut laden' }}
    </button>
  </div>
</template>

<style scoped>
.container {
  padding: 1rem;
  border: 2px solid #42b883;
  border-radius: 8px;
  font-family: sans-serif;
  max-width: 260px;
  background: white;
}
.url-label {
  font-size: 0.72rem;
  font-family: monospace;
  color: #42b883;
  margin-bottom: 0.6rem;
  font-weight: 600;
}
.status {
  padding: 0.5rem 0.75rem;
  border-radius: 4px;
  font-size: 0.9rem;
  margin-bottom: 0.6rem;
}
.loading { background: #f0faf5; color: #42b883; }
.error { background: #fff5f5; color: #c53030; }
.resp-label {
  font-size: 0.72rem;
  color: #999;
  margin-bottom: 0.25rem;
}
.json {
  background: #f0faf5;
  padding: 0.6rem;
  border-left: 3px solid #42b883;
  border-radius: 4px;
  font-size: 0.7rem;
  margin-bottom: 0.75rem;
  white-space: pre-wrap;
  color: #333;
  line-height: 1.5;
}
.btn {
  background: #42b883;
  color: white;
  border: none;
  padding: 0.4rem 0.9rem;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.85rem;
  width: 100%;
  transition: opacity 0.15s;
}
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
.btn:not(:disabled):hover { opacity: 0.87; }
</style>
