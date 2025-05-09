<template>
  <footer class="bg-gray-50 py-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center mb-8">
        <div class="flex items-center gap-2 mb-6 md:mb-0">
          <Palette class="h-6 w-6 text-indigo-600" />
          <span class="text-xl font-bold bg-gradient-to-r from-indigo-600 to-violet-600 bg-clip-text text-transparent">
            ColorLift
          </span>
        </div>

        <div class="flex flex-wrap justify-center gap-x-8 gap-y-4">
          <a href="#features" class="text-gray-600 hover:text-indigo-600 transition-colors"> Features </a>
          <a href="#palettes" class="text-gray-600 hover:text-indigo-600 transition-colors"> Palettes </a>
          <a href="#how-it-works" class="text-gray-600 hover:text-indigo-600 transition-colors"> How It Works </a>
          <a href="#install" class="text-gray-600 hover:text-indigo-600 transition-colors"> Install </a>
          <a
            href="https://github.com/yourusername/colorlift"
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
            href="https://github.com/yourusername/colorlift"
            target="_blank"
            rel="noopener"
            class="text-gray-400 hover:text-gray-600 transition-colors"
          >
            <Github class="h-5 w-5" />
          </a>
          <a
            href="https://twitter.com/colorlift"
            target="_blank"
            rel="noopener"
            class="text-gray-400 hover:text-gray-600 transition-colors"
          >
            <Twitter class="h-5 w-5" />
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { Palette, Twitter, Github } from "lucide-vue-next";

const currentYear = computed(() => new Date().getFullYear());
</script>
