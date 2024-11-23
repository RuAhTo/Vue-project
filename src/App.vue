<script setup lang="ts">
import { ref, onMounted } from 'vue';
import Navbar from './components/Navbar.vue';
import Hero from './components/Hero.vue';
import Carousel from './components/Carousel.vue';

// Reaktiva variabler
const activePage = ref(0);
const pages = ref([]);

// Funktion för att hämta sidor
const getPages = async () => {
  const res = await fetch('pages.json');
  const data = await res.json();
  pages.value = data; // Uppdatera den reaktiva variabeln
};

// Kör funktionen vid montering av komponenten
onMounted(() => {
  getPages();
});
</script>

<template>
  <Navbar
    :pages="pages"
    :active-page="activePage"
    :nav-link-click="(index) => activePage = index"
  ></Navbar>
  <Hero />
  <Carousel />
</template>

<style>
</style>

