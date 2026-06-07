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
