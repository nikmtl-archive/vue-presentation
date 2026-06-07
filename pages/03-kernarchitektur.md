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
zoom: 0.82
---

# Kernarchitektur: Props & Emits

**Props** fließen von Parent → Kind &nbsp;·&nbsp; **Emits** fließen von Kind → Parent

<div class="grid grid-cols-2 gap-6 mt-4">
<img src="/vue_reactivity_flow.svg" alt="Vue Reaktivitätszyklus" class=" w-full object-contain" />
<div class="grid grid-rows-2 gap-3">

```vue {1,4-5,11}
<!-- Parent.vue -->
<template>
  <UserCard
    :name="userName"
    @update:name="userName = $event"
  />
</template>

<script setup>
import { ref } from 'vue'
const userName = ref('Anna')
</script>
```

```vue {1,3-4,8-9}
<!-- UserCard.vue (Kind) -->
<script setup>
const props = defineProps({ name: String })
const emit = defineEmits(['update:name'])
</script>

<template>
  <p>{{ props.name }}</p>
  <button @click="emit('update:name', 'Max')">
    Namen ändern
  </button>
</template>


```

</div>
</div>
