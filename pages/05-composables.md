---
zoom: 0.85
---

# Composables – das useXxx-Pattern

<v-clicks>

Composables kapseln und **teilen** reaktive Logik zwischen beliebig vielen Komponenten

</v-clicks>

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

<v-clicks>

**Warum Composables?**

</v-clicks>

<v-clicks>

- Mixins (Vue 2) hatten Namenskonflikte und unklare Herkunft der Eigenschaften
- Composables sind **explizit**: klar, woher jede Variable kommt
- Konvention: Dateiname und Funktionsname beginnen mit `use`
- native TypeScript Unterstützung

</v-clicks>

</div>
<div v-click="1">

```js 
// composables/useFetch.js
import { ref } from 'vue'

export function useFetch(url) {
  const data = ref(null)
  const error = ref(null)
  const loading = ref(true)

  fetch(url)
    .then(r => r.json())
    .then(json => { data.value = json })
    .catch(err => { error.value = err })
    .finally(() => { loading.value = false })

  return { data, error, loading }
}
```

```vue
<!--components/FetchDemo.vue-->
<script setup>
import { useFetch } from './useFetch'

const { data, error, loading } = useFetch('/api/users')
</script>
```

</div>
</div>

<!--
Composables folgen der React-Hooks-Logik konzeptuell, sind aber nicht an Rendering-Zyklen gebunden.
Man kann Composables in anderen Composables nutzen – echte Komposierbarkeit.
-->

---
zoom: 0.85
---

# Composables – useFetch in Aktion

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

```vue
<script setup>
import { useFetch } from './composables/useFetch'

// One line – all reactive states bundled
const {
  data,
  loading,
  error,
  reload,
} = useFetch(
  'https://jsonplaceholder.typicode.com/todos/1'
)
</script>

<template>
  <!-- v-if / v-else-if: state control -->
  <div v-if="loading">Loading...</div>
  <pre v-else-if="data">
    {{ JSON.stringify(data, null, 2) }}
  </pre>
  <div v-else-if="error">
    Error: {{ error }}
  </div>
  <button @click="reload">Reload</button>
</template>
```

</div>
<div>

<div class="flex flex-col items-center justify-center h-full gap-4">
  <div class="text-sm text-gray-400">Live-Demo:</div>
  <FetchDemo />
</div>

</div>
</div>

<!--
Das ist der Kern des Composable-Patterns: die gesamte Fetch-Logik ist in einer Funktion.
Die Komponente ist schlank und deklarativ – dieselbe useFetch-Funktion läuft in beliebig vielen Komponenten.
-->
