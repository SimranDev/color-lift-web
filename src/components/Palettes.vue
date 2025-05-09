<template>
  <section id="palettes" class="py-20">
    <div class="container mx-auto px-4">
      <div class="text-center max-w-3xl mx-auto mb-16">
        <h2 class="heading-secondary">Popular Color Palettes at Your Fingertips</h2>
        <p class="subtitle">Access a wide range of professionally curated color systems</p>
      </div>

      <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
        <div
          v-for="(palette, index) in colorPalettes"
          :key="index"
          class="bg-white rounded-xl shadow-sm overflow-hidden border border-gray-100 hover:shadow-md transition-all duration-300"
        >
          <div class="h-2 flex">
            <div
              v-for="(color, colorIndex) in palette.colors"
              :key="colorIndex"
              class="flex-1 h-full"
              :style="{ backgroundColor: color }"
            ></div>
          </div>
          <div class="p-6">
            <div class="flex justify-between items-center mb-4">
              <h3 class="text-lg font-semibold">{{ palette.name }}</h3>
              <span class="px-3 py-1 bg-gray-100 text-xs rounded-full">{{ palette.colorCount }} colors</span>
            </div>
            <p class="text-gray-600 text-sm mb-4">{{ palette.description }}</p>

            <div class="mt-4">
              <div class="grid grid-cols-5 gap-2">
                <div v-for="i in 5" :key="i" class="h-8 rounded" :style="{ backgroundColor: palette.preview[i - 1] }"></div>
              </div>
              <div class="flex justify-between items-center mt-4">
                <span class="text-xs text-gray-500">Sample swatches shown</span>
                <button
                  class="text-indigo-600 text-sm font-medium hover:text-indigo-700 transition-colors flex items-center"
                  @click="toggleColorInfo(palette.id)"
                >
                  <span>View details</span>
                  <ChevronDown v-if="!expandedPalette[palette.id]" class="h-4 w-4 ml-1" />
                  <ChevronUp v-else class="h-4 w-4 ml-1" />
                </button>
              </div>
            </div>

            <div v-if="expandedPalette[palette.id]" class="mt-4 pt-4 border-t border-gray-100">
              <div class="grid grid-cols-2 gap-4">
                <div v-for="(detail, detailIndex) in palette.details" :key="detailIndex" class="flex items-center">
                  <div class="w-4 h-4 rounded mr-2" :style="{ backgroundColor: detail.color }"></div>
                  <span class="text-xs">{{ detail.name }}</span>
                  <button class="ml-auto text-gray-400 hover:text-indigo-600" @click="copyColor(detail.color)">
                    <Copy class="h-3 w-3" />
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { reactive } from "vue";
import { ChevronDown, ChevronUp, Copy } from "lucide-vue-next";

interface PaletteDetail {
  name: string;
  color: string;
}

interface ColorPalette {
  id: number;
  name: string;
  colorCount: number;
  description: string;
  colors: string[];
  preview: string[];
  details: PaletteDetail[];
}

const expandedPalette = reactive<Record<number, boolean>>({});

const colorPalettes: ColorPalette[] = [
  {
    id: 1,
    name: "Tailwind CSS",
    colorCount: 110,
    description: "A utility-first CSS framework with a carefully crafted color system",
    colors: ["#0ea5e9", "#14b8a6", "#8b5cf6", "#f59e0b", "#ef4444"],
    preview: ["#bfdbfe", "#60a5fa", "#3b82f6", "#1d4ed8", "#1e3a8a"],
    details: [
      { name: "blue-100", color: "#dbeafe" },
      { name: "blue-300", color: "#93c5fd" },
      { name: "blue-500", color: "#3b82f6" },
      { name: "blue-700", color: "#1d4ed8" },
      { name: "blue-900", color: "#1e3a8a" },
      { name: "red-500", color: "#ef4444" },
      { name: "green-500", color: "#22c55e" },
      { name: "purple-500", color: "#8b5cf6" },
    ],
  },
  {
    id: 2,
    name: "Material UI",
    colorCount: 280,
    description: "Google's Material Design color system used in Android and web apps",
    colors: ["#f44336", "#e91e63", "#9c27b0", "#673ab7", "#3f51b5"],
    preview: ["#bbdefb", "#90caf9", "#64b5f6", "#42a5f5", "#2196f3"],
    details: [
      { name: "blue-100", color: "#bbdefb" },
      { name: "blue-300", color: "#64b5f6" },
      { name: "blue-500", color: "#2196f3" },
      { name: "blue-700", color: "#1976d2" },
      { name: "blue-900", color: "#0d47a1" },
      { name: "red-500", color: "#f44336" },
      { name: "purple-500", color: "#9c27b0" },
      { name: "green-500", color: "#4caf50" },
    ],
  },
  {
    id: 3,
    name: "Radix Colors",
    colorCount: 180,
    description: "An open-source color system for designing beautiful, accessible websites",
    colors: ["#006adc", "#30a46c", "#e54666", "#9a5fc0", "#eaac0f"],
    preview: ["#c2f0ff", "#89daff", "#2eaaff", "#0080ff", "#0060df"],
    details: [
      { name: "blue-3", color: "#c2f0ff" },
      { name: "blue-6", color: "#89daff" },
      { name: "blue-9", color: "#0080ff" },
      { name: "blue-11", color: "#0060df" },
      { name: "red-9", color: "#e54666" },
      { name: "green-9", color: "#30a46c" },
      { name: "purple-9", color: "#9a5fc0" },
      { name: "amber-9", color: "#eaac0f" },
    ],
  },
  {
    id: 4,
    name: "Open Color",
    colorCount: 130,
    description: "An open-source color scheme optimized for UI components",
    colors: ["#fa5252", "#ff922b", "#fab005", "#40c057", "#339af0"],
    preview: ["#d0ebff", "#a5d8ff", "#74c0fc", "#4dabf7", "#339af0"],
    details: [
      { name: "blue-2", color: "#d0ebff" },
      { name: "blue-4", color: "#a5d8ff" },
      { name: "blue-6", color: "#74c0fc" },
      { name: "blue-8", color: "#339af0" },
      { name: "red-8", color: "#fa5252" },
      { name: "green-8", color: "#40c057" },
      { name: "orange-8", color: "#ff922b" },
      { name: "yellow-8", color: "#fab005" },
    ],
  },
  {
    id: 5,
    name: "Flat UI Colors",
    colorCount: 40,
    description: "Beautiful flat colors that work great in modern designs",
    colors: ["#1abc9c", "#3498db", "#9b59b6", "#f1c40f", "#e74c3c"],
    preview: ["#3498db", "#2980b9", "#e74c3c", "#c0392b", "#1abc9c"],
    details: [
      { name: "Turquoise", color: "#1abc9c" },
      { name: "Emerald", color: "#2ecc71" },
      { name: "Peter River", color: "#3498db" },
      { name: "Amethyst", color: "#9b59b6" },
      { name: "Wet Asphalt", color: "#34495e" },
      { name: "Sun Flower", color: "#f1c40f" },
      { name: "Carrot", color: "#e67e22" },
      { name: "Alizarin", color: "#e74c3c" },
    ],
  },
  {
    id: 6,
    name: "Nord",
    colorCount: 16,
    description: "An arctic, north-bluish color palette for elegant interfaces",
    colors: ["#8fbcbb", "#88c0d0", "#81a1c1", "#5e81ac", "#bf616a"],
    preview: ["#eceff4", "#e5e9f0", "#d8dee9", "#4c566a", "#2e3440"],
    details: [
      { name: "Polar Night 1", color: "#2e3440" },
      { name: "Polar Night 2", color: "#3b4252" },
      { name: "Polar Night 3", color: "#434c5e" },
      { name: "Polar Night 4", color: "#4c566a" },
      { name: "Snow Storm 1", color: "#d8dee9" },
      { name: "Frost 1", color: "#8fbcbb" },
      { name: "Frost 2", color: "#88c0d0" },
      { name: "Aurora Red", color: "#bf616a" },
    ],
  },
];

const toggleColorInfo = (id: number) => {
  expandedPalette[id] = !expandedPalette[id];
};

const copyColor = (color: string) => {
  navigator.clipboard.writeText(color);

  // Could add a toast notification here
  console.log(`Copied ${color} to clipboard`);
};
</script>
