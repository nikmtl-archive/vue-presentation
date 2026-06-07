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

# Vue Router

<div class="grid grid-cols-2 gap-6 mt-6">

<div>

**Routen definieren**

```ts
const routes = [
  { path: '/', component: Home },
  { path: '/about', component: About },
  {
    path: '/user/:id',
    component: UserProfile,
    children: [
      { path: 'posts', component: UserPosts }
    ]
  }
]
```

</div>

<div class="flex flex-col gap-4 mt-2">

<v-click>
<div class="flex items-start gap-3">
  <lucide-route class="text-2xl text-[#42b883] mt-0.5 shrink-0" />
  <div>
    <p class="font-bold text-sm text-[#2d8a63]">Dynamische Segmente</p>
    <p class="text-xs text-gray-500"><code>:id</code> im Pfad – per <code>useRoute().params.id</code> abrufbar</p>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3">
  <lucide-shield class="text-2xl text-[#42b883] mt-0.5 shrink-0" />
  <div>
    <p class="font-bold text-sm text-[#2d8a63]">Navigation Guards</p>
    <p class="text-xs text-gray-500"><code>beforeEach</code> – Auth-Checks vor jedem Routenwechsel</p>
  </div>
</div>
</v-click>

<v-click>
<div class="flex items-start gap-3">
  <lucide-package class="text-2xl text-[#42b883] mt-0.5 shrink-0" />
  <div>
    <p class="font-bold text-sm text-[#2d8a63]">Lazy Loading</p>
    <p class="text-xs text-gray-500"><code>() => import('./Page.vue')</code> – Komponente wird erst bei Bedarf geladen</p>
  </div>
</div>
</v-click>

</div>

</div>

<!--
Vue Router ist der offizielle Router für Vue.js.
Navigation per <RouterLink> im Template, programmatisch mit useRouter().push().
-->

