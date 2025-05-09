<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="{ 'bg-white/80 backdrop-blur-md shadow-sm': scrolled, 'bg-transparent': !scrolled }"
  >
    <div class="container mx-auto px-4 py-4 flex justify-between items-center">
      <div class="flex items-center gap-2">
        <Palette class="h-6 w-6 text-indigo-600" />
        <span class="text-xl font-bold bg-gradient-to-r from-indigo-600 to-violet-600 bg-clip-text text-transparent">
          ColorLift
        </span>
      </div>

      <div class="hidden md:flex space-x-8">
        <a
          v-for="(item, index) in navItems"
          :key="index"
          :href="item.href"
          class="text-gray-600 hover:text-indigo-600 transition-colors"
        >
          {{ item.label }}
        </a>
      </div>

      <a href="#install" class="btn-primary"> Install Extension </a>

      <button class="md:hidden text-gray-600" @click="toggleMobileMenu">
        <Menu v-if="!mobileMenuOpen" class="h-6 w-6" />
        <X v-else class="h-6 w-6" />
      </button>
    </div>

    <!-- Mobile menu -->
    <div
      v-if="mobileMenuOpen"
      class="md:hidden bg-white py-4 px-4 shadow-md absolute w-full transition-all duration-300"
      style="top: 100%"
    >
      <div class="flex flex-col space-y-4">
        <a
          v-for="(item, index) in navItems"
          :key="index"
          :href="item.href"
          class="text-gray-600 hover:text-indigo-600 transition-colors py-2"
          @click="closeMobileMenu"
        >
          {{ item.label }}
        </a>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { Palette, Menu, X } from "lucide-vue-next";

const scrolled = ref(false);
const mobileMenuOpen = ref(false);

const navItems = [
  { label: "Features", href: "#features" },
  { label: "Palettes", href: "#palettes" },
  { label: "How It Works", href: "#how-it-works" },
];

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;
};

const closeMobileMenu = () => {
  mobileMenuOpen.value = false;
};

const handleScroll = () => {
  scrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  handleScroll(); // Check initial scroll position
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>
