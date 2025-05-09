<template>
  <section class="pt-32 pb-20 px-4 overflow-hidden relative">
    <!-- Background gradient elements -->
    <div class="absolute -top-24 -left-24 w-96 h-96 bg-indigo-200 rounded-full opacity-20 blur-3xl"></div>
    <div class="absolute -bottom-24 -right-24 w-96 h-96 bg-violet-200 rounded-full opacity-20 blur-3xl"></div>

    <div class="container mx-auto">
      <div class="flex flex-col lg:flex-row gap-12 items-center">
        <div class="flex-1 max-w-xl">
          <h1 class="heading-primary">
            Quick access to
            <span class="bg-gradient-to-r from-indigo-600 to-violet-600 bg-clip-text text-transparent">color palettes</span> for
            everyone
          </h1>
          <p class="subtitle mt-6">
            Access popular design system colors like Material UI, Tailwind, and Radix directly in your browser. Perfect for
            developers and designers working with Figma, VS Code, or any design tool.
          </p>
          <div class="mt-10 flex flex-col sm:flex-row gap-4">
            <a href="#install" class="btn-primary">Install Extension</a>
            <a
              href="https://github.com/SimranDev/color-lift"
              target="_blank"
              rel="noopener"
              class="btn-secondary flex items-center gap-2"
            >
              <Github class="h-4 w-4" />
              <span>View on GitHub</span>
            </a>
          </div>
          <div class="mt-8 flex items-center text-gray-500 text-sm flex-wrap gap-4">
            <div class="flex items-center">
              <Check class="h-4 w-4 text-green-500 mr-2" />
              <span>Free & Open Source</span>
            </div>
            <div class="flex items-center">
              <Chrome class="h-4 w-4 mr-2" />
              <span>Chrome extension</span>
            </div>
            <div class="flex items-center">
              <Users class="h-4 w-4 mr-2" />
              <span>Community driven</span>
            </div>
          </div>
        </div>
        <div class="flex-1 relative">
          <div class="relative z-10 bg-white rounded-xl shadow-2xl overflow-hidden border border-gray-100">
            <div class="h-10 bg-gray-100 flex items-center px-4 gap-2">
              <div class="flex space-x-2">
                <div class="w-3 h-3 rounded-full bg-red-500"></div>
                <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
                <div class="w-3 h-3 rounded-full bg-green-500"></div>
              </div>
              <div class="text-xs text-gray-500 ml-2">ColorLift Extension</div>
            </div>
            <div class="p-6">
              <div class="mb-4">
                <h3 class="text-sm font-medium mb-2">Tailwind CSS</h3>
                <div class="grid grid-cols-10 gap-2">
                  <div
                    v-for="(color, i) in tailwindBlueColors"
                    :key="i"
                    class="color-swatch group cursor-pointer relative"
                    :style="{ backgroundColor: color.hex }"
                    @mouseenter="activeColor = color"
                    @mouseleave="activeColor = null"
                  >
                    <div
                      v-if="activeColor === color"
                      class="absolute bottom-full left-1/2 transform -translate-x-1/2 mb-2 px-3 py-1 bg-gray-900 text-white text-xs rounded whitespace-nowrap"
                    >
                      {{ color.hex }} {{ color.name }}
                    </div>
                  </div>
                </div>
              </div>
              <div>
                <h3 class="text-sm font-medium mb-2">Material UI</h3>
                <div class="grid grid-cols-10 gap-2">
                  <div
                    v-for="(color, i) in muiPurpleColors"
                    :key="i"
                    class="color-swatch group cursor-pointer relative"
                    :style="{ backgroundColor: color.hex }"
                    @mouseenter="activeColor = color"
                    @mouseleave="activeColor = null"
                  >
                    <div
                      v-if="activeColor === color"
                      class="absolute bottom-full left-1/2 transform -translate-x-1/2 mb-2 px-3 py-1 bg-gray-900 text-white text-xs rounded whitespace-nowrap"
                    >
                      {{ color.hex }} {{ color.name }}
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <!-- Decorative elements -->
          <div id="anim-infinity" class="absolute -bottom-10 -right-10 w-32 h-32 bg-indigo-100 rounded-xl rotate-12 z-0"></div>
          <div id="anim-infinity-2" class="absolute -top-20 -left-20 w-20 h-20 bg-violet-100 rounded-xl -rotate-12 z-0"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";
import { Check, Chrome, Github, Users } from "lucide-vue-next";

interface ColorSwatch {
  name: string;
  hex: string;
}

const tailwindBlueColors = [
  { name: "blue-50", hex: "#eff6ff" },
  { name: "blue-100", hex: "#dbeafe" },
  { name: "blue-200", hex: "#bfdbfe" },
  { name: "blue-300", hex: "#93c5fd" },
  { name: "blue-400", hex: "#60a5fa" },
  { name: "blue-500", hex: "#3b82f6" },
  { name: "blue-600", hex: "#2563eb" },
  { name: "blue-700", hex: "#1d4ed8" },
  { name: "blue-800", hex: "#1e40af" },
  { name: "blue-900", hex: "#1e3a8a" },
];

const muiPurpleColors = [
  { name: "purple-50", hex: "#f5f3ff" },
  { name: "purple-100", hex: "#ede9fe" },
  { name: "purple-200", hex: "#ddd6fe" },
  { name: "purple-300", hex: "#c4b5fd" },
  { name: "purple-400", hex: "#a78bfa" },
  { name: "purple-500", hex: "#8b5cf6" },
  { name: "purple-600", hex: "#7c3aed" },
  { name: "purple-700", hex: "#6d28d9" },
  { name: "purple-800", hex: "#5b21b6" },
  { name: "purple-900", hex: "#4c1d95" },
];

const activeColor = ref<ColorSwatch | null>(null);
</script>

<style scoped>
.color-swatch {
  @apply h-8 rounded transition-transform duration-200 relative;
}

.color-swatch:hover {
  @apply transform scale-110 z-10 shadow-md;
}

#anim-infinity {
  animation: moveInfinity 15s linear infinite;
}

#anim-infinity-2 {
  animation: moveInfinity 25s linear infinite;
}
</style>
