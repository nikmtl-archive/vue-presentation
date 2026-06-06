---
theme: seriph
title: "Vue.js 3 – Ein modernes Frontend-Framework"
transition: slide-left
comark: true
drawings:
  persist: false
themeConfig:
  primary: '#42b883'
---

# Vue.js 3

**Ein modernes Frontend-Framework**

<div class="text-lg mt-4 opacity-70">Für Informatikstudenten und Webentwickler</div>

<div class="abs-br m-8 text-sm opacity-40">2026</div>

<!--
Herzlich willkommen. In den nächsten zehn Minuten schauen wir uns Vue.js 3 an –
was es ist, wie es funktioniert, und wann es die richtige Wahl ist.
-->

---
layout: default
---

# Was ist Vue.js?

Ein **progressives JavaScript-Framework** für den Aufbau von Benutzeroberflächen.

<v-clicks>

- **Progressiv** – von einem einfachen Widget bis zur vollständigen SPA skalierbar; kein Alles-oder-nichts
- **Deklarativ** – die UI ist eine Funktion des Zustands; kein manuelles DOM-Manipulieren nötig
- **Komponentenbasiert** – wiederverwendbare, gekapselte Bausteine mit eigenem Template, Logik und Style

</v-clicks>

<v-click>

### Kurze Geschichte

| Version | Jahr | Highlight |
|---------|------|-----------|
| Vue 1.x | 2014 | Evan You (ex-Google) – erstes öffentliches Release |
| Vue 2.x | 2016 | Options API, weltweite Adoption, Vuex |
| **Vue 3.x** | **2020** | **Composition API, TypeScript-first, Vite** |

</v-click>

<!--
Evan You arbeitete bei Google mit AngularJS und wollte nur die "guten Teile" davon extrahieren.
Vue 3 ist der aktuelle Standard und der Fokus dieser Präsentation.
-->

---
layout: default
---

# Kernarchitektur

<v-clicks>

**Virtual DOM**
Vue rendert nicht direkt ins echte DOM. Änderungen werden zunächst in einer leichtgewichtigen In-Memory-Repräsentation berechnet (Diffing), bevor nur die minimal nötigen echten DOM-Operationen ausgeführt werden.

**Reactivity System**
`ref()` und `reactive()` machen Daten reaktiv – über JavaScript Proxies. Vue verfolgt automatisch, welche Komponenten welche Daten lesen. Ändert sich ein Wert, werden ausschließlich betroffene Komponenten neu gerendert.

**Component-Modell**
Jede Komponente kapselt Template, Logik und Styles. Daten fließen per **Props** hinein und per **Emits** hinaus. Gemeinsame Logik wird in **Composables** ausgelagert.

</v-clicks>

<!--
Das Reactivity System basiert in Vue 3 auf ES Proxies – anders als in Vue 2 (Object.defineProperty).
Das erlaubt reaktives Tracking für Arrays, Maps und dynamisch hinzugefügte Properties.
-->

---
layout: two-cols
---

# Single File Components

Eine `.vue`-Datei vereint alles in einer Datei:

```vue
<template>
  <!-- Deklaratives HTML mit Vue-Direktiven -->
  <h1>{{ titel }}</h1>
  <button @click="grüßen">Klick mich</button>
</template>

<script setup>
// Composition API – empfohlener Stil in Vue 3
import { ref } from 'vue'

const titel = ref('Hallo, Vue!')

function grüßen() {
  alert(titel.value)
}
</script>

<style scoped>
/* CSS ist nur für diese Komponente gültig */
h1 { color: #42b883; }
</style>
```

::right::

<div class="mt-6 space-y-4 pl-4">

<div v-click class="p-3 rounded border-l-4 border-[#42b883] bg-green-50">
  <div class="font-bold text-[#42b883] mb-1">&lt;template&gt;</div>
  <div class="text-sm text-gray-600">Deklaratives HTML. Direktbindung an reaktive Daten – Vue aktualisiert das DOM automatisch.</div>
</div>

<div v-click class="p-3 rounded border-l-4 border-blue-400 bg-blue-50">
  <div class="font-bold text-blue-600 mb-1">&lt;script setup&gt;</div>
  <div class="text-sm text-gray-600">Composition API mit weniger Boilerplate. Alles, was hier deklariert wird, steht im Template zur Verfügung.</div>
</div>

<div v-click class="p-3 rounded border-l-4 border-purple-400 bg-purple-50">
  <div class="font-bold text-purple-600 mb-1">&lt;style scoped&gt;</div>
  <div class="text-sm text-gray-600">CSS ist auf diese Komponente beschränkt. Kein Namensraum-Problem, keine globalen Kollisionen.</div>
</div>

</div>

<!--
SFCs werden zur Build-Zeit (via Vite) vom Vue-Compiler verarbeitet.
`script setup` ist seit Vue 3.2 der empfohlene Stil – weniger Zeilen, klarer Scope.
-->

---
layout: two-cols
---

# Options API vs. Composition API

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

::right::

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
  <strong>Fazit:</strong> Options API ist einsteigerfreundlicher. Composition API erlaubt bessere Wiederverwendbarkeit, TypeScript-Integration und Feature-zentrierte Organisation.
</div>

<!--
Options API: Logik nach "Optionen" gruppiert (data, methods, computed).
Composition API: Logik nach Feature gruppiert – alles, was zu einem Feature gehört, steht beieinander.
Beide APIs sind in Vue 3 vollständig unterstützt – kein Zwang zur Migration.
-->

---
layout: two-cols
zoom: 0.9
---

# Codebeispiel 1 – Reaktive Komponente

```vue {1-3|5-7|9-11|13-22|all}
<script setup>
import { ref, computed } from 'vue'

// ref(): reaktiver Zustand
const count = ref(0)
const multiplikator = ref(2)

// computed(): automatisch neu berechnet
const ergebnis = computed(
  () => count.value * multiplikator.value
)
</script>

<template>
  <!-- v-model: bidirektionale Bindung -->
  <input
    v-model.number="multiplikator"
    type="number"
  />
  <!-- @click: Event-Handler -->
  <button @click="count++">+1</button>
  <!-- {{ }}: Template-Interpolation -->
  <p>{{ count }} × {{ multiplikator }} = {{ ergebnis }}</p>
</template>
```

::right::

<div class="flex flex-col items-center justify-center h-full gap-4">
  <div class="text-sm text-gray-400">Live-Demo:</div>
  <ReactiveCounter />
</div>

<!--
ref() erzeugt ein reaktives Objekt mit .value-Eigenschaft.
computed() ist gecacht – wird nur neu berechnet, wenn eine seiner Abhängigkeiten sich ändert.
v-model ist Kurzschreibweise für :value + @input (Two-Way Binding).
-->

---
layout: default
---

# Direktiven in Aktion

Vue-Direktiven sind spezielle Attribute mit dem `v-`-Präfix:

<div class="grid grid-cols-2 gap-8 mt-4">
<div>

| Direktive | Zweck |
|-----------|-------|
| `v-bind` (`:`) | Attribut an Datenwert binden |
| `v-model` | Zwei-Wege-Datenbindung |
| `v-for` | Liste über Array rendern |
| `v-if` / `v-show` | Bedingtes Rendern |
| `v-on` (`@`) | Event-Handler registrieren |

<div class="mt-4 text-sm text-gray-500">
  <code>v-if</code> entfernt das Element aus dem DOM.<br/>
  <code>v-show</code> setzt nur <code>display: none</code>.
</div>

</div>
<div>

**Live: v-model + computed + v-for**

<LiveFilter />

</div>
</div>

<!--
v-bind und v-on haben Kurzformen: : und @
v-model bei React würde onChange + value separat erfordern – Vue macht das automatisch.
Die LiveFilter-Komponente demonstriert v-model, computed und v-for zusammen in Aktion.
-->

---
layout: two-cols-header
zoom: 0.92
---

# Composables – das useXxx-Pattern

Composables kapseln und **teilen** reaktive Logik zwischen beliebig vielen Komponenten.

::left::

**Warum Composables?**

<v-clicks>

- Mixins (Vue 2) hatten Namenskonflikte und unklare Herkunft der Eigenschaften
- Composables sind **explizit**: klar, woher jede Variable kommt
- Konvention: Dateiname und Funktionsname beginnen mit `use`
- Vollständig typsicher mit TypeScript

</v-clicks>

::right::

```js {1-2|4-8|10-20|22-23}
// composables/useFetch.js
import { ref } from 'vue'

export function useFetch(url) {
  const daten = ref(null)
  const laedt = ref(true)
  const fehler = ref(null)

  async function abrufen() {
    laedt.value = true
    fehler.value = null
    try {
      const antwort = await fetch(url)
      daten.value = await antwort.json()
    } catch (e) {
      fehler.value = e.message
    } finally {
      laedt.value = false
    }
  }

  abrufen() // Sofort beim Einbinden ausführen
  return { daten, laedt, fehler, erneut: abrufen }
}
```

<!--
Composables folgen der React-Hooks-Logik konzeptuell, sind aber nicht an Rendering-Zyklen gebunden.
Man kann Composables in anderen Composables nutzen – echte Komposierbarkeit.
-->

---
layout: two-cols
zoom: 0.9
---

# Codebeispiel 2 – useFetch in Aktion

```vue {1-3|5-8|10-21|all}
<script setup>
import { useFetch } from './composables/useFetch'

// Eine Zeile – alle reaktiven Zustände gebündelt
const {
  daten,
  laedt,
  fehler,
  erneut,
} = useFetch(
  'https://jsonplaceholder.typicode.com/todos/1'
)
</script>

<template>
  <!-- v-if / v-else-if: Zustandssteuerung -->
  <div v-if="laedt">Lädt...</div>
  <pre v-else-if="daten">
    {{ JSON.stringify(daten, null, 2) }}
  </pre>
  <div v-else-if="fehler">
    Fehler: {{ fehler }}
  </div>
  <button @click="erneut">Erneut laden</button>
</template>
```

::right::

<div class="flex flex-col items-center justify-center h-full gap-4">
  <div class="text-sm text-gray-400">Live-Demo:</div>
  <FetchDemo />
</div>

<!--
Das ist der Kern des Composable-Patterns: die gesamte Fetch-Logik ist in einer Funktion.
Die Komponente ist schlank und deklarativ – dieselbe useFetch-Funktion läuft in beliebig vielen Komponenten.
-->

---
layout: default
---

# Das Vue-Ökosystem

<v-clicks>

**Vite** – Build-Tool und Dev-Server
Nutzt native ES-Module im Browser – kein vollständiges Bundling während der Entwicklung. Sofortiger Start, blitzschnelles Hot Module Replacement. Vue-Projekte und Vite entstammen beide von Evan You.

**Pinia** – State Management
Offizieller Nachfolger von Vuex. Store-Definition mit Composition API, vollständige TypeScript-Unterstützung, nahtlose Vue DevTools-Integration. Kein Boilerplate, keine Mutation-Typen.

**Vue Router** – Client-side Routing
Offizieller Router für SPA-Navigation. Unterstützt verschachtelte Routen, Navigation Guards, Lazy Loading und den HTML5-History-Modus.

**Vue DevTools** – Browser-Extension
Zeigt den Komponentenbaum, reaktive Zustände, Events und Performance-Profile in Echtzeit. Unverzichtbar beim Entwickeln.

</v-clicks>

<!--
Der gesamte Stack – Vite + Vue + Pinia + Router – ist aufeinander abgestimmt und hochoptimiert.
Für neue Projekte: `npm create vue@latest` richtet alles automatisch ein.
-->

---
layout: two-cols
---

# Stärken & Schwächen

**Vorteile**

<v-clicks>

- Sanfte Lernkurve – exzellente, mehrsprachige Dokumentation auf vuejs.org
- Flexibel: Options API für Einsteiger, Composition API für komplexe Logik
- Leichtgewichtig (~34 kB gzip) und performant
- Moderne Toolchain: Vite, Pinia, DevTools
- `v-model` ermöglicht Two-Way Binding ohne manuellen Aufwand

</v-clicks>

::right::

**Nachteile**

<v-clicks>

- Kleineres Ökosystem als React – weniger Drittanbieter-Komponenten
- Geringere Enterprise-Adoption; weniger Stellenanzeigen als React oder Angular
- Composition API ist initial ungewohnt für Einsteiger ohne Hooks-Erfahrung
- Weniger Backing von Tech-Konzernen – geringere Sichtbarkeit in bestimmten Branchen

</v-clicks>

<!--
Ehrliche Einschätzung: Vue ist technisch exzellent, kämpft aber mit der Wahrnehmung als "kleines Framework".
In der asiatischen Region – v.a. China – ist Vue sehr stark verbreitet.
-->

---
layout: default
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
  Vue.js 3 ist eine <span style="color: #42b883; font-weight: bold;">ausgezeichnete Wahl</span> für:
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

<div class="mt-10 text-2xl font-light" style="color: #42b883;">
  Fragen?
</div>

<!--
vuejs.org hat eine der besten Dokumentationen im Frontend-Ökosystem.
Der interaktive Tutorial auf vuejs.org/tutorial ist besonders empfehlenswert zum Einstieg.
-->
