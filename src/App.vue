<script setup>
import { ref } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

// Reactive variables
const message = ref('Hello Vue 3!');
const isVisible = ref(true);
const inputText = ref('');
const count = ref(0);

// Methods
const increment = () => {
  count.value++;
};

const toggleVisibility = () => {
  isVisible.value = !isVisible.value;
};
</script>

<template>
  <div class="container">
    <!-- Text Interpolation -->
    <h1>{{ message }}</h1>

    <!-- Conditional Rendering -->
    <button @click="toggleVisibility">
      {{ isVisible ? 'Sembunyikan' : 'Tampilkan' }} Teks
    </button>
    <p v-if="isVisible">Teks ini bisa disembunyikan</p>

    <!-- Form Binding -->
    <input v-model="inputText" placeholder="Ketik sesuatu..." />
    <p>Isi input: {{ inputText }}</p>

    <!-- Event Listener -->
    <button @click="increment">Tambah</button>
    <p>Hitungan: {{ count }}</p>

    <!-- Attribute Binding -->
    <a :href="'https://vite.dev'" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />    </a>
    <a :href="'https://vuejs.org/'" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  
  <!-- Using HelloWorld component -->
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.container {
  padding: 1rem;
}
.logo {
  width: 50px;
  height: 50px;
  margin: 10px;
  transition: transform 0.3s;
}
.logo:hover {
  transform: scale(1.1);
}
button {
  padding: 0.5rem 1rem;
  margin: 0.5rem 0;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
button:hover {
  background-color: #36936d;
}
input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 5px;
}
</style>