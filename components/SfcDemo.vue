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
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}
h2 {
  margin: 0;
  color: #2d8a63;
}
input, button {
  padding: 0.3rem 0.6rem;
  border-radius: 4px;
  border: 1px solid #ccc;
  font-size: 0.9rem;
}
button {
  background: #42b883;
  color: white;
  border-color: #42b883;
  cursor: pointer;
}
</style>
