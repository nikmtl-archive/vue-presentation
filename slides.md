---
theme: apple-basic
layout: intro
title: "Vue.js 3 – Ein modernes Frontend-Framework"
colorSchema: 'light'
---

<img src="/vue-logo.svg" class="absolute top-8 right-12 h-28 opacity-90 drop-shadow-lg" />

# Vue

Eine Einführung in Vue.js 3

<div class="absolute bottom-10 text-sm font-500 text-gray-400">
  Dominik Mitzel, Michelle Niedersberg · Web Engineering II · 2026
</div>

<!--
Wir schauen uns an:
- Was ist Vue
- Wie Funktioniert
- Wann richtige Wahl
-->

---

# Was ist Vue.js

<v-click>
  <p class="text-center text-xl text-gray-900 pt-16">Ein <strong> JavaScript-Framework</strong> für Frontend-UIs</p>
</v-click>

<div class="grid grid-cols-3 gap-6 mt-12">

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-layers class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Progressiv</p>
    <p class="text-sm text-gray-500 mt-1">Simpel Starten <br /> → Tools und Features hinzufügen <br /> → komplexe Web Apps </p>
  </div>
</v-click>
  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-code-2 class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Deklarativ</p>
    <p class="text-sm text-gray-500 mt-1">TEXT VERBESSERN</p>
  </div>
  </v-click>

<v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-box class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Komponentenbasiert</p>
    <p class="text-sm text-gray-500 mt-1">TEXT VERBESSERN</p>
  </div>
  </v-click>
</div>


<!--
Die UI ist eine Funktion des Zustands – kein manuelles DOM-Manipulieren, nur State beschreiben.
Hauptkonzept von Vue.js: Wiederverwendbare, gekapselte Bausteine mit eigenem Template, Logik und Style.


Click 1: Subtitle – progressives Framework
Click 2: 3 Spalten – Progressiv / Deklarativ / Komponentenbasiert
-->

---

# Was ist Vue.js

Kurz: Entstehung und Historischer Überblick 

<div class="flex flex-col mt-15 items-center">

<div class="overflow-x-auto w-full max-w-3xl">

| Version | Jahr | Highlight |
|---------|------|-----------|
| Vue 1.x | 2014 | Evan You (ex-Google) – erstes öffentliches Release |
| Vue 2.x | 2016 | Options API, weltweite Adoption, Vuex |
| **Vue 3.x** | **2020** | **Composition API, TypeScript-first, Vite** |

</div>

<div class="mt-4 text-sm text-gray-500 text-center">
  Aktuell ist Vue 3 der Standard – wir konzentrieren uns heute auf die neuen Features und Best Practices von Vue 3.
</div>

</div>

<!--
Evan You arbeitete bei Google mit AngularJS und wollte nur die "guten Teile" davon extrahieren.
Vue 3 ist der aktuelle Standard und der Fokus dieser Präsentation.
-->


---

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

---

# Kernarchitektur
Was macht Vue im Hintergrund?

<div class="grid grid-cols-3 gap-6 mt-10">

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-layers class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Virtual DOM</p>
    <p class="text-sm text-gray-500 mt-1">Änderungen werden zuerst in einer In-Memory-Repräsentation berechnet (Diffing) – nur minimal nötige DOM-Operationen werden ausgeführt.</p>
  </div>
  </v-click>

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-activity class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Reactivity System</p>
    <p class="text-sm text-gray-500 mt-1"><code>ref()</code> und <code>reactive()</code> nutzen JS Proxies. Vue trackt automatisch Abhängigkeiten – nur betroffene Komponenten werden neu gerendert.</p>
  </div>
  </v-click>

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-box class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Komponentenmodell</p>
    <p class="text-sm text-gray-500 mt-1">Template, Logik und Styles in einer Einheit. Daten fließen per <strong>Props</strong> rein, per <strong>Emits</strong> raus. Logik wird in <strong>Composables</strong> ausgelagert.</p>
  </div>
  </v-click>

</div>

<!--
Das Reactivity System basiert in Vue 3 auf ES Proxies – anders als in Vue 2 (Object.defineProperty).
Das erlaubt reaktives Tracking für Arrays, Maps und dynamisch hinzugefügte Properties.
-->

---
zoom: 0.88
hide: true
---

# Options API vs. Composition API TODO

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

**Options API** (klassisch / Vue 2)

```vue
<script>
export default {
  data() {
    return { count: 0 }
  },
  computed: {
    doubled() {
      return this.count * 2
    }
  },
  methods: {
    increment() {
      this.count++
    }
  }
}
</script>
```

</div>
<div>

**Composition API** (Vue 3 / empfohlen)

```vue
<script setup>
import { ref, computed } from 'vue'

// Zustand
const count = ref(0)

// Abgeleiteter Wert (gecacht)
const doubled = computed(
  () => count.value * 2
)

// Methode
function increment() {
  count.value++
}
</script>
```

<div v-click class="mt-3 p-3 rounded border border-[#42b883] bg-green-50 text-sm">
  <strong>Fazit:</strong> Composition API erlaubt bessere Wiederverwendbarkeit, TypeScript-Integration und Feature-zentrierte Organisation.
</div>

</div>
</div>

<!--
Options API: Logik nach "Optionen" gruppiert (data, methods, computed).
Composition API: Logik nach Feature gruppiert – alles, was zu einem Feature gehört, steht beieinander.
Beide APIs sind in Vue 3 vollständig unterstützt – kein Zwang zur Migration.
-->


---
zoom: 0.85
hide: true
---

# Codebeispiel 1 – Reaktive Komponente

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

```vue {1-3|5-7|9-11|13-22|all}
<script setup>
import { ref, computed } from 'vue'

// ref(): reactive state
const count = ref(0)
const multiplier = ref(2)

// computed(): automatically recalculated
const result = computed(
  () => count.value * multiplier.value
)
</script>

<template>
  <!-- v-model: two-way binding -->
  <input
    v-model.number="multiplier"
    type="number"
  />
  <!-- @click: event handler -->
  <button @click="count++">+1</button>
  <!-- {{ }}: template interpolation -->
  <p>{{ count }} × {{ multiplier }} = {{ result }}</p>
</template>
```

</div>
<div>

<div class="flex flex-col items-center justify-center h-full gap-4">
  <div class="text-sm text-gray-400">Live-Demo:</div>
  <ReactiveCounter />
</div>

</div>
</div>

<!--
ref() erzeugt ein reaktives Objekt mit .value-Eigenschaft.
computed() ist gecacht – wird nur neu berechnet, wenn eine seiner Abhängigkeiten sich ändert.
v-model ist Kurzschreibweise für :value + @input (Two-Way Binding).
-->

---


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
-->

---
zoom: 0.85
---

# Composables – das useXxx-Pattern

Composables kapseln und **teilen** reaktive Logik zwischen beliebig vielen Komponenten

<div class="grid grid-cols-2 gap-6 mt-2">
<div>

**Warum Composables?**

<v-clicks>

- Mixins (Vue 2) hatten Namenskonflikte und unklare Herkunft der Eigenschaften
- Composables sind **explizit**: klar, woher jede Variable kommt
- Konvention: Dateiname und Funktionsname beginnen mit `use`
- native TypeScript Unterstützung

</v-clicks>

</div>
<div>

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

---

# Das Vue-Ökosystem

<div class="grid grid-cols-2 gap-6 mt-8">

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-zap class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Vite</p>
    <p class="text-xs text-gray-500 mt-1">Build-Tool & Dev-Server. Nutzt native ES-Module – kein Bundling in der Entwicklung. Sofortiger Start, blitzschnelles HMR.</p>
  </div>
  </v-click>

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-database class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Pinia</p>
    <p class="text-xs text-gray-500 mt-1">State Management. Offizieller Vuex-Nachfolger. Composition API, TypeScript-first, kein Boilerplate.</p>
  </div>
  </v-click>

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-route class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Vue Router</p>
    <p class="text-xs text-gray-500 mt-1">Client-side Routing. Verschachtelte Routen, Navigation Guards, Lazy Loading und HTML5-History-Modus.</p>
  </div>
  </v-click>

  <v-click>
  <div class="flex flex-col items-center text-center">
    <lucide-wrench class="text-4xl mb-2 text-[#42b883]" />
    <p class="font-bold text-[#2d8a63] tracking-wide uppercase text-sm mt-2">Vue DevTools</p>
    <p class="text-xs text-gray-500 mt-1">Browser-Extension. Komponentenbaum, reaktive Zustände, Events und Performance-Profile in Echtzeit.</p>
  </div>
  </v-click>

</div>

<!--
Der gesamte Stack – Vite + Vue + Pinia + Router – ist aufeinander abgestimmt und hochoptimiert.
Für neue Projekte: `npm create vue@latest` richtet alles automatisch ein.
-->

---

# Stärken & Schwächen

<div class="grid grid-cols-2 gap-6 mt-4">

<div>
  <div class="flex items-center gap-2 mb-3">
    <span class="font-bold text-[#2d8a63]">Stärken</span>
  </div>
  <div class="flex flex-col gap-2">

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-book-open class="text-[#42b883] mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Sanfte Lernkurve</div>
      <div class="text-xs text-gray-500">Exzellente, mehrsprachige Doku auf vuejs.org</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-code-2 class="text-[#42b883] mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Moderne Composition API</div>
      <div class="text-xs text-gray-500">Reaktive Logik klar strukturiert, TypeScript-first, Composables</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-zap class="text-[#42b883] mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Leichtgewichtig & schnell</div>
      <div class="text-xs text-gray-500">~34 kB gzip · Virtual DOM · minimale Re-Renders</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-wrench class="text-[#42b883] mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Moderne Toolchain</div>
      <div class="text-xs text-gray-500">Vite · Pinia · Vue Router · DevTools – alles abgestimmt</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-users class="text-[#42b883] mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Unabhängig & Community-getrieben</div>
      <div class="text-xs text-gray-500">Keine erzwungenen Breaking Changes · Roadmap ohne Corporate-Agenda</div>
    </div>
  </div>
  </v-click>

  </div>
</div>

<div>
  <div class="flex items-center gap-2 mb-3">
    <span class="font-bold text-red-500">Schwächen</span>
  </div>
  <div class="flex flex-col gap-2">

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-package class="text-red-400 mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Kleineres Ökosystem</div>
      <div class="text-xs text-gray-500">Weniger Drittanbieter-Bibliotheken als React</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-briefcase class="text-red-400 mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Geringere Marktdurchdringung</div>
      <div class="text-xs text-gray-500">Weniger Stellenanzeigen · kleinerer Talent-Pool beim Hiring</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-building-2 class="text-red-400 mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Kein Enterprise-First-Ansatz</div>
      <div class="text-xs text-gray-500">Keine LTS-Garantien, kein dedizierter Support – CTOs wählen React (Meta) oder Angular (Google)</div>
    </div>
  </div>
  </v-click>

  <v-click>
  <div class="flex items-start gap-3 px-3 py-2">
    <lucide-landmark class="text-red-400 mt-0.5 shrink-0 text-base" />
    <div>
      <div class="font-semibold text-sm text-gray-800">Kein Tech-Konzern-Backing</div>
      <div class="text-xs text-gray-500">Community-Projekt ohne Google/Meta-Absicherung – geringere Akzeptanz in Enterprise-Branchen</div>
    </div>
  </div>
  </v-click>

  </div>
</div>

</div>

<!--
Ehrliche Einschätzung: Vue ist technisch exzellent, kämpft aber mit der Wahrnehmung als "kleines Framework".
In der asiatischen Region – v.a. China – ist Vue sehr stark verbreitet.
-->

---
class: text-sm
---

# Abgrenzung: Vue vs. React vs. Angular vs. Svelte

<div class="mt-4">

| | **Vue 3** | **React** | **Angular** | **Svelte** |
|---|---|---|---|---|
| **Syntax** | Template + opt. JSX | JSX | Template | Template |
| **TypeScript** | Optional | Optional | Pflicht | Optional |
| **Datenbindung** | Two-Way (`v-model`) | One-Way + Handler | Two-Way (`ngModel`) | Two-Way |
| **Lernkurve** | Flach | Mittel | Steil | Flach |
| **Laufzeit-Gewicht** | ~34 kB | ~40 kB | ~130 kB | Minimal |
| **Ökosystem** | Mittel | Sehr groß | Groß | Klein |
| **Backing** | Community / Evan You | Meta | Google | Community |

</div>

<v-click>

**Kernunterschied**: Vue und Svelte sind template-basiert und näher an HTML. React erfordert JSX und ein funktionales Denkmodell. Angular ist ein vollständiges Framework mit Meinungen zu allem. Svelte hat keine Runtime – der Compiler erzeugt reines JavaScript.

</v-click>

<!--
Two-Way Binding ist kein Alleinstellungsmerkmal – Angular hat das auch.
Der konzeptionelle Unterschied zu React ist größer: Vue denkt in Templates und Reaktivität, React in Funktionen und State.
Svelte ist elegant, aber das deutlich kleinste Ökosystem.
-->

---
layout: center
class: text-center
---

# Fazit & Einsatzempfehlung

<div class="text-xl mt-4 mb-8">
  Vue.js 3 ist eine <span class="text-[#42b883] font-bold">ausgezeichnete Wahl</span> für:
</div>

<div class="grid grid-cols-3 gap-4 text-left max-w-3xl mx-auto">

<div v-click class="p-4 rounded border-2 border-[#42b883] bg-green-50">
  <div class="font-bold mb-2 text-[#42b883]">Einsteiger</div>
  <div class="text-sm text-gray-600">Options API bietet einen klaren Einstiegspunkt. Exzellente Doku, flache Lernkurve, überschaubares Ökosystem.</div>
</div>

<div v-click class="p-4 rounded border-2 border-[#42b883] bg-green-50">
  <div class="font-bold mb-2 text-[#42b883]">Mittelgroße Apps</div>
  <div class="text-sm text-gray-600">Composition API + Pinia skalieren gut. Kein unnötiges Boilerplate, TypeScript-Unterstützung inklusive.</div>
</div>

<div v-click class="p-4 rounded border-2 border-[#42b883] bg-green-50">
  <div class="font-bold mb-2 text-[#42b883]">Schnelle Projekte</div>
  <div class="text-sm text-gray-600">Vite + Vue = sofortige Produktivität. Ideal für Prototypen, Semesterprojekte und interaktive Demos.</div>
</div>

</div>

<div v-click class="mt-8 text-sm text-gray-400">
  Für Enterprise-Umgebungen mit bestehendem React- oder Angular-Team: andere Wahl sorgfältig abwägen.
</div>

<!--
Kurz: Wenn ihr neu anfangt und flexibel seid, ist Vue ein sehr angenehmes Framework zum Lernen und Entwickeln.
Wenn ihr in ein bestehendes React-Team kommt, lohnt sich Vue-Wissen trotzdem – die Konzepte sind nahezu identisch.
-->

---
layout: center
class: text-center
---

# Quellen & weiterführende Links

<div class="grid grid-cols-2 gap-8 mt-8 max-w-2xl mx-auto text-left text-sm">

<div>

**Offizielle Dokumentation**
- [vuejs.org](https://vuejs.org) – Vue 3 Dokumentation & Tutorial
- [pinia.vuejs.org](https://pinia.vuejs.org) – State Management
- [router.vuejs.org](https://router.vuejs.org) – Vue Router
- [vite.dev](https://vite.dev) – Build Tool

</div>

<div>

**Diese Präsentation**
- Erstellt mit [Slidev](https://sli.dev)
- Codebeispiele: Vue 3 + Composition API
- Interaktive Demos: Live in Vue

**Schnellstart**
```bash
npm create vue@latest
```

</div>

</div>

<div class="mt-10 text-2xl font-light text-[#42b883]">
  Fragen?
</div>

<!--
vuejs.org hat eine der besten Dokumentationen im Frontend-Ökosystem.
Der interaktive Tutorial auf vuejs.org/tutorial ist besonders empfehlenswert zum Einstieg.
-->
