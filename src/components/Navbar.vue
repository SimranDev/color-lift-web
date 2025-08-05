<template>
  <nav
    class="fixed top-0 left-0 right-0 z-50 transition-all duration-300"
    :class="{ 'bg-white/80 backdrop-blur-md shadow-sm': scrolled, 'bg-transparent': !scrolled }"
  >
    <div class="container mx-auto px-4 py-4 flex justify-between items-center">
      <div class="flex items-center gap-2">
        <img src="/src/assets/logo.png" alt="ColorLift" class="h-8 md:h-10" />
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

      <div class="hidden md:flex space-x-3">
        <a
          href="https://chromewebstore.google.com/detail/colorlift/pdlbgfbmijdmejbmjababcdblgpipgdn"
          class="flex items-center gap-2 px-4 py-2.5 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm hover:shadow-md"
          title="Install for Chrome"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="/src/assets/chrome.png" alt="Chrome" class="h-5 w-5" />
          Chrome
        </a>
        <a
          href="http://addons.mozilla.org/en-US/firefox/addon/colorlift/"
          class="flex items-center gap-2 px-4 py-2.5 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm hover:shadow-md"
          title="Install for Firefox"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="/src/assets/firefox.webp" alt="Firefox" class="h-5 w-5" />
          Firefox
        </a>
        <a
          href="https://github.com/SimranDev/color-lift"
          class="flex items-center gap-2 px-4 py-2.5 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm hover:shadow-md"
          title="View on GitHub"
          target="_blank"
          rel="noopener noreferrer"
        >
          <img src="/src/assets/github.png" alt="GitHub" class="h-5 w-5" />
          Open Source
        </a>
      </div>

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
        <div class="pt-2 border-t border-gray-200">
          <a
            href="https://github.com/SimranDev/color-lift-web"
            class="flex items-center justify-center gap-2 px-4 py-3 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 mb-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm"
            target="_blank"
            rel="noopener noreferrer"
            @click="closeMobileMenu"
          >
            <img src="/src/assets/github.png" alt="GitHub" class="h-5 w-5" />
            Open Source
          </a>
          <a
            href="https://chromewebstore.google.com/detail/colorlift/pdlbgfbmijdmejbmjababcdblgpipgdn"
            class="flex items-center justify-center gap-2 px-4 py-3 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 mb-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm"
            target="_blank"
            rel="noopener noreferrer"
            @click="closeMobileMenu"
          >
            <img src="/src/assets/chrome.png" alt="Chrome" class="h-5 w-5" />
            Install for Chrome
          </a>
          <a
            href="http://addons.mozilla.org/en-US/firefox/addon/colorlift/"
            class="flex items-center justify-center gap-2 px-4 py-3 text-sm font-medium text-gray-700 bg-white border border-gray-200 rounded-full hover:bg-gray-50 hover:border-gray-300 transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 shadow-sm"
            target="_blank"
            rel="noopener noreferrer"
            @click="closeMobileMenu"
          >
            <img src="/src/assets/firefox.webp" alt="Firefox" class="h-5 w-5" />
            Install for Firefox
          </a>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";
import { Menu, X } from "lucide-vue-next";

const scrolled = ref(false);
const mobileMenuOpen = ref(false);

const navItems = [
  { label: "Features", href: "#features" },
  { label: "Palettes", href: "#palettes" },
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
