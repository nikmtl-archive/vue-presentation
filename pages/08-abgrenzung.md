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
