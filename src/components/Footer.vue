<template>
  <footer class="bg-gray-50 py-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center mb-8">
        <div class="flex items-center gap-2 mb-6 md:mb-0" id="logo-section">
          <img src="/src/assets/logo.png" alt="ColorLift" class="h-5 md:h-7" />
        </div>

        <div class="flex flex-wrap justify-center gap-x-8 gap-y-4">
          <a href="#features" class="text-gray-600 hover:text-indigo-600 transition-colors"> Features </a>
          <a href="#palettes" class="text-gray-600 hover:text-indigo-600 transition-colors"> Palettes </a>
          <a
            href="https://github.com/SimranDev/color-lift"
            target="_blank"
            rel="noopener"
            class="text-gray-600 hover:text-indigo-600 transition-colors"
          >
            GitHub
          </a>
        </div>
      </div>

      <div class="border-t border-gray-200 pt-8 flex flex-col md:flex-row justify-between items-center">
        <div class="text-gray-500 text-sm mb-4 md:mb-0">© {{ currentYear }} ColorLift. Open source and free to use.</div>

        <div class="flex items-center space-x-4">
          <a
            href="https://github.com/SimranDev/color-lift"
            target="_blank"
            rel="noopener"
            class="text-gray-400 hover:text-gray-600 transition-colors"
          >
            <img src="/src/assets/github.png" alt="GitHub" class="h-5 w-5" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed } from "vue";

const currentYear = computed(() => new Date().getFullYear());
</script>
