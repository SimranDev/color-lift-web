<template>
  <section id="how-it-works" class="py-20 bg-gray-50">
    <div class="container mx-auto px-4">
      <div class="text-center max-w-3xl mx-auto mb-16">
        <h2 class="heading-secondary">How ColorLift Works</h2>
        <p class="subtitle">Simple, intuitive, and designed for speed</p>
      </div>

      <div class="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto">
        <div v-for="(step, index) in steps" :key="index" class="relative">
          <!-- Step number -->
          <div
            class="w-12 h-12 rounded-full bg-indigo-600 text-white flex items-center justify-center text-xl font-bold mb-6 relative z-10 mx-auto"
          >
            {{ index + 1 }}
          </div>

          <!-- Connecting line -->
          <div
            v-if="index < steps.length - 1"
            class="hidden md:block absolute top-6 left-[calc(50%+2rem)] right-0 h-0.5 bg-indigo-200 z-0 transform -translate-y-1/2"
          ></div>

          <!-- Content -->
          <div class="text-center">
            <h3 class="text-xl font-semibold mb-3">{{ step.title }}</h3>
            <p class="text-gray-600">{{ step.description }}</p>
          </div>
        </div>
      </div>

      <!-- Demo Sections -->
      <div class="mt-16 max-w-4xl mx-auto relative overflow-hidden">
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
              <div class="grid grid-cols-5 sm:grid-cols-8 lg:grid-cols-10 gap-1 sm:gap-2">
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
              <div class="grid grid-cols-5 sm:grid-cols-8 lg:grid-cols-10 gap-1 sm:gap-2">
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
        <div
          id="anim-infinity"
          class="absolute -bottom-6 -right-6 w-24 h-24 lg:w-32 lg:h-32 lg:-bottom-10 lg:-right-10 bg-indigo-100 rounded-xl rotate-12 z-0"
        ></div>
        <div
          id="anim-infinity-2"
          class="absolute -top-6 -left-6 w-16 h-16 lg:w-20 lg:h-20 lg:-top-20 lg:-left-20 bg-violet-100 rounded-xl -rotate-12 z-0"
        ></div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface ColorSwatch {
  name: string;
  hex: string;
}

const steps = [
  {
    title: "Install the Extension",
    description: "Add ColorLift to Chrome from the Web Store with just one click.",
  },
  {
    title: "Click the ColorLift Icon",
    description: "Access your favorite color palettes instantly from any webpage.",
  },
  {
    title: "Copy & Use Colors",
    description: "Grab colors in your preferred format (HEX, RGB) with one click.",
  },
];

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
@reference "tailwindcss";

.extension-popup {
  transform-origin: top right;
}

.extension-icon {
  cursor: pointer;
  transition: transform 0.2s;
}

.extension-icon:hover {
  transform: scale(1.05);
}

.animate-fade-in {
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

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
