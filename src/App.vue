<template>
  <div class="app">
    <Navbar />
    <main>
      <Hero />
      <Features />
      <Palettes />
      <HowItWorks />
      <CTA />
    </main>
    <Footer />
  </div>
</template>

<script setup lang="ts">
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import Features from "./components/Features.vue";
import Palettes from "./components/Palettes.vue";
import HowItWorks from "./components/HowItWorks.vue";
import CTA from "./components/CTA.vue";
import Footer from "./components/Footer.vue";
</script>
