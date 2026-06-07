# Components
Kernkonzept von Vue

<div class="grid grid-cols-2 gap-6 mt-2">
<div v-click="'1'">

```vue {all|6-10|1-4|13-16|all}
<template>


</template>


<script setup>
 

</script>


<style scoped>
  

</style>
```


</div>
<div>

<div class="mt-1 space-y-10">

<div v-click="'2'" class="p-3 rounded border-l-4 border-[#42b883] bg-green-50 flex items-center justify-between">
  <div>
    <div class="font-bold text-[#42b883] mb-1">&lt;template&gt;</div>
    <div class="text-sm text-gray-600">HTML UI Elemente - Reaktive Datenbindung an State</div>
  </div>
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/61/HTML5_logo_and_wordmark.svg" class="h-8 opacity-70" />
</div>

<div v-click="'1'" class="p-3 rounded border-l-4 border-blue-400 bg-blue-50 flex items-center justify-between">
  <div>
    <div class="font-bold text-blue-600 mb-1">&lt;script setup&gt;</div>
    <div class="text-sm text-gray-600">Daten und Logik – State Management</div>
  </div>
  <img src="https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png" class="h-8 opacity-70" />
</div>

<div v-click="'3'" class="p-3 rounded border-l-4 border-purple-400 bg-purple-50 flex items-center justify-between">
  <div>
    <div class="font-bold text-purple-600 mb-1">&lt;style scoped&gt;</div>
    <div class="text-sm text-gray-600">Stylings (scoped → für diese Komponente)</div>
  </div>
  <img src="https://upload.wikimedia.org/wikipedia/commons/d/d5/CSS3_logo_and_wordmark.svg" class="h-8 opacity-70" />
</div>

</div>

</div>
</div>

<div v-after class="text-center mt-4">
  <span class="font-bold text-blue-500">Daten</span> bleiben stets <span class="font-bold">synchronisiert</span> mit der <span class="font-bold text-[#42b883]">UI</span> 
  <p> Gleiche Eingaben erzeugen immer dieselbe Ausgabe → deklaratives Paradigma </p>
</div>

---
zoom: 0.85
---

# SFC – Erstes Beispiel
Single File Component – alles in einer Datei: Template, Script, Style

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

```vue {all|12-13|3,5|all}
<template>
  <div class="card">
    <h2>Hello, {{ name }}!</h2>
    <input v-model="name"/>
    <button @click="count++">Clicked: {{ count }}×</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('World')
const count = ref(0)
</script>

<style scoped>
.card {
  padding: 1rem;
  border: 1px solid #42b883;
  border-radius: 8px;
}
</style>
```

</div>
<div class="flex flex-col gap-3 justify-center h-full">

<div v-click="1" class="p-2 rounded-lg border-l-4 border-blue-400 bg-blue-50 text-xs">
  <div class="font-bold text-blue-700 mb-0.5">① Script – declare data</div>
  <code class="text-blue-600">const name = ref('World')</code>
</div>

<div v-click="1" class="flex flex-col items-center gap-0 text-gray-300 leading-none">
  <span class="text-lg">↓</span>
  <span v-click="2" class="text-[10px] text-gray-400 -mt-1">reaktiv gebunden</span>
</div>

<div v-click="2" class="p-2 rounded-lg border-l-4 border-[#42b883] bg-green-50 text-xs">
  <div class="font-bold text-[#2d8a63] mb-0.5">② Template – display data</div>
  <code v-pre class="text-green-700">{{ name }} · {{ count }}</code>
  <div class="text-gray-400 mt-0.5">Data changes → Template updates</div>
</div>

<div v-click="3" class="p-2 rounded-lg border-l-4 border-amber-400 bg-amber-50 text-xs">
  <div class="font-bold text-amber-700">③ Reactivity</div>
  <div class="text-gray-500 mt-0.5">Vue re-renders automatically</div>
</div>

<div v-click class="mt-auto text-xs text-gray-400 text-center">Live-Demo:</div>
<SfcDemo v-after />

</div>
</div>
