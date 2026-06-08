---
zoom: 0.85
---

# Composables – das useXxx-Pattern
<v-clicks>

Composables **kapseln und teilen reaktive Logik** zwischen beliebig vielen Komponenten

</v-clicks>

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

<v-click>

**Warum Composables?**

</v-click>

<div class="flex flex-col gap-2 mt-2">

<v-click>
<div class="flex items-start gap-3 px-3 py-2">
  <lucide-git-branch class="text-[#42b883] mt-0.5 shrink-0 text-base" />
  <div>
    <div class="font-semibold text-sm text-gray-800">Logik auslagern</div>
    <div class="text-xs text-gray-500">Logik in mehreren Komponenten wiederverwendbar</div>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3 px-3 py-2">
  <lucide-share-2 class="text-[#42b883] mt-0.5 shrink-0 text-base" />
  <div>
    <div class="font-semibold text-sm text-gray-800">Reaktiv</div>
    <div class="text-xs text-gray-500">Composables haben vollen Zugriff auf alle reaktiven Features</div>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3 px-3 py-2">
  <lucide-eye class="text-[#42b883] mt-0.5 shrink-0 text-base" />
  <div>
    <div class="font-semibold text-sm text-gray-800">Explizit & nachvollziehbar</div>
    <div class="text-xs text-gray-500">Klar, woher jede Variable kommt</div>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3 px-3 py-2">
  <lucide-file-code class="text-[#42b883] mt-0.5 shrink-0 text-base" />
  <div>
    <div class="font-semibold text-sm text-gray-800">Konvention: <code>use</code>-Prefix</div>
    <div class="text-xs text-gray-500">Dateiname und Funktionsname beginnen mit <code>use</code></div>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3 px-3 py-2">
  <lucide-shield-check class="text-[#42b883] mt-0.5 shrink-0 text-base" />
  <div>
    <div class="font-semibold text-sm text-gray-800">TypeScript-first</div>
    <div class="text-xs text-gray-500">Native TypeScript Unterstützung</div>
  </div>
</div>
</v-click>

</div>

</div>
<div v-click="8">

```js 
// composables/useFetch.js
import { ref } from 'vue'

export function useFetch(url) {
  const data = ref(null)
  const error = ref(null)
  const loading = ref(false)

  async function load() {
    loading.value = true
    data.value = await fetch(url).then(r => r.json())
    loading.value = false
  }

  return { data, error, loading, load }
}
```

```vue
<!--components/FetchDemo.vue-->
<script setup>
import { useFetch } from './useFetch'

const { data, error, loading, load } = useFetch('/api/users')
</script>
```

</div>
</div>

<!--
TODO: Tiefere Recherche was warum wie?

Dominik
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

const {
  data,
  loading,
  error,
  load,
} = useFetch(
  'https://jsonplaceholder.typicode.com/todos/1'
)
</script>

<template>
  <div v-if="loading">Loading...</div>
  <pre v-else-if="data">
    {{ JSON.stringify(data, null, 2) }}
  </pre>
  <div v-else-if="error">
    Error: {{ error }}
  </div>
  <button @click="load">
    {{ data ? 'Reload' : 'Laden' }}
  </button>
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
Dominik
-->
