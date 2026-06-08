<script setup>
import { ref } from 'vue'

function useFetch(url) {
  const data = ref(null)
  const loading = ref(false)
  const error = ref(null)

  async function load() {
    loading.value = true
    error.value = null
    data.value = null
    try {
      const response = await fetch(url)
      if (!response.ok) throw new Error(`HTTP ${response.status}`)
      data.value = await response.json()
    } catch (e) {
      error.value = e.message
    } finally {
      loading.value = false
    }
  }

  return { data, loading, error, load }
}

const { data, loading, error, load } = useFetch(
  'https://jsonplaceholder.typicode.com/todos/1'
)
</script>

<template>
  <div class="container">
    <div class="url-label">GET /todos/1</div>

    <div v-if="loading" class="status loading">Loading...</div>
    <div v-else-if="error" class="status error">Error: {{ error }}</div>
    <div v-else-if="data">
      <div class="resp-label">Response:</div>
      <pre class="json">{{ JSON.stringify(data, null, 2) }}</pre>
    </div>

    <button
      @click="load"
      :disabled="loading"
      class="btn"
    >
      {{ loading ? 'Loading...' : data ? 'Reload' : 'Laden' }}
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
