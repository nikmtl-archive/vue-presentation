# Direktiven in Aktion

Vue-Direktiven sind spezielle Attribute mit dem `v-`-Präfix:

<div class="grid grid-cols-2 gap-6 mt-4">
<div class="relative" style="min-height:220px">

<div v-click.hide="1" class="absolute inset-0">

| Direktive | Zweck |
|-----------|-------|
| `v-bind` (`:`) | Attribut an Datenwert binden |
| `v-model` | Zwei-Wege-Datenbindung |
| `v-for` | Liste über Array rendern |
| `v-if` / `v-show` | Bedingtes Rendern |
| `v-on` (`@`) | Event-Handler registrieren |

<div class="mt-3 text-sm text-gray-500">
  <code>v-if</code> entfernt das Element aus dem DOM.<br/>
  <code>v-show</code> setzt nur <code>display: none</code>.
</div>

</div>

<div v-click="1" class="absolute inset-0 flex flex-col gap-2 ">
  <div class="text-sm font-semibold text-gray-500">Live-Demo</div>
  <LiveFilter />
</div>

</div>
<div>

```vue {13-14,16-17,19-20}
<script setup>
const query = ref('')
const concepts = ['Reactivity', 'Composables',
                  'Directives', 'Vue Router', 'Pinia']
const filtered = computed(() =>
  concepts.filter(k =>
    k.toLowerCase().includes(query.value.toLowerCase())
  )
)
</script>

<template>
  <!-- v-model: two-way binding -->
  <input v-model="query" placeholder="Search..." />

  <!-- v-for + v-bind(:key) -->
  <li v-for="k in filtered" :key="k">{{ k }}</li>

  <!-- v-if: conditional rendering -->
  <div v-if="!filtered.length">No results</div>
</template>
```

</div>
</div>

<!--
v-bind und v-on haben Kurzformen: : und @
v-model bei React würde onChange + value separat erfordern – Vue macht das automatisch.
Die LiveFilter-Komponente demonstriert v-model, computed und v-for zusammen in Aktion.

Michelle
-->
