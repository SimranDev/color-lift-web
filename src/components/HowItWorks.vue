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

      <!-- Demo animation -->
      <div class="mt-20 max-w-4xl mx-auto bg-white rounded-xl shadow-md overflow-hidden">
        <div class="demo-browser-header h-10 bg-gray-100 flex items-center px-4 gap-2">
          <div class="flex space-x-2">
            <div class="w-3 h-3 rounded-full bg-red-500"></div>
            <div class="w-3 h-3 rounded-full bg-yellow-500"></div>
            <div class="w-3 h-3 rounded-full bg-green-500"></div>
          </div>
          <div class="text-xs text-gray-500 ml-2">Using ColorLift Extension</div>
        </div>

        <div class="p-8 relative h-80 overflow-hidden flex items-center justify-center">
          <div class="demo-animation">
            <div
              class="extension-icon absolute top-4 right-4 h-10 w-10 flex items-center justify-center bg-white rounded shadow-md cursor-pointer"
              @click="startDemo"
            >
              <Palette class="h-6 w-6 text-indigo-600" />
            </div>

            <!-- Extension popup (shows when clicked) -->
            <div
              class="extension-popup absolute top-16 right-4 w-80 bg-white rounded-lg shadow-xl border border-gray-200 p-4 opacity-0 scale-95 transition-all duration-300"
              :class="{ 'opacity-100 scale-100': demoActive }"
            >
              <div class="flex justify-between items-center mb-4">
                <div class="flex items-center">
                  <Palette class="h-5 w-5 text-indigo-600 mr-2" />
                  <h3 class="font-medium">ColorLift</h3>
                </div>
                <div class="flex space-x-2">
                  <button class="text-gray-400 hover:text-gray-600">
                    <Settings class="h-4 w-4" />
                  </button>
                  <button class="text-gray-400 hover:text-gray-600" @click="stopDemo">
                    <X class="h-4 w-4" />
                  </button>
                </div>
              </div>

              <!-- Palette selector -->
              <div class="mb-4">
                <div class="relative">
                  <select
                    class="block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md"
                    v-model="selectedPalette"
                  >
                    <option v-for="option in paletteOptions" :key="option.value" :value="option.value">
                      {{ option.label }}
                    </option>
                  </select>
                </div>
              </div>

              <!-- Color swatches -->
              <div class="space-y-3">
                <div v-for="(group, groupIndex) in currentPaletteColors" :key="groupIndex">
                  <div class="text-xs font-medium text-gray-500 mb-1">{{ group.name }}</div>
                  <div class="grid grid-cols-10 gap-1">
                    <div
                      v-for="(color, colorIndex) in group.colors"
                      :key="colorIndex"
                      class="h-6 rounded cursor-pointer group relative"
                      :style="{ backgroundColor: color.hex }"
                      @mouseenter="hoveredColor = color"
                      @mouseleave="hoveredColor = null"
                      @click="selectColor(color)"
                    ></div>
                  </div>
                </div>
              </div>

              <!-- Selected color details -->
              <div v-if="selectedColor" class="mt-4 p-3 bg-gray-50 rounded-lg">
                <div class="flex items-center justify-between">
                  <div class="flex items-center">
                    <div class="w-8 h-8 rounded mr-3" :style="{ backgroundColor: selectedColor.hex }"></div>
                    <div>
                      <div class="text-sm font-medium">{{ selectedColor.name }}</div>
                      <div class="text-xs text-gray-500">{{ selectedColor.hex }}</div>
                    </div>
                  </div>
                  <div class="flex space-x-1">
                    <button class="p-1.5 rounded hover:bg-gray-200 transition-colors" @click="copyColorFormat('hex')">
                      <div class="text-xs font-mono">HEX</div>
                    </button>
                    <button class="p-1.5 rounded hover:bg-gray-200 transition-colors" @click="copyColorFormat('rgb')">
                      <div class="text-xs font-mono">RGB</div>
                    </button>
                  </div>
                </div>

                <!-- Copy notification -->
                <div v-if="showCopied" class="mt-2 text-center text-xs text-green-600 animate-fade-in">
                  <div class="flex items-center justify-center">
                    <Check class="h-3 w-3 mr-1" />
                    <span>{{ copiedFormat.toUpperCase() }} copied to clipboard!</span>
                  </div>
                </div>
              </div>

              <!-- Tooltip -->
              <div
                v-if="hoveredColor && !selectedColor"
                class="absolute -top-10 left-1/2 transform -translate-x-1/2 px-3 py-1.5 bg-gray-900 text-white text-xs rounded whitespace-nowrap"
              >
                {{ hoveredColor.name }}: {{ hoveredColor.hex }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import { Palette, Settings, X, Check } from "lucide-vue-next";

interface ColorOption {
  name: string;
  hex: string;
  rgb: string;
}

interface ColorGroup {
  name: string;
  colors: ColorOption[];
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

const demoActive = ref(false);
const selectedPalette = ref("tailwind");
const hoveredColor = ref<ColorOption | null>(null);
const selectedColor = ref<ColorOption | null>(null);
const showCopied = ref(false);
const copiedFormat = ref("");

const paletteOptions = [
  { label: "Tailwind CSS", value: "tailwind" },
  { label: "Material UI", value: "mui" },
  { label: "Radix Colors", value: "radix" },
];

const tailwindColors: ColorGroup[] = [
  {
    name: "Blue",
    colors: [
      { name: "blue-50", hex: "#eff6ff", rgb: "rgb(239, 246, 255)" },
      { name: "blue-100", hex: "#dbeafe", rgb: "rgb(219, 234, 254)" },
      { name: "blue-200", hex: "#bfdbfe", rgb: "rgb(191, 219, 254)" },
      { name: "blue-300", hex: "#93c5fd", rgb: "rgb(147, 197, 253)" },
      { name: "blue-400", hex: "#60a5fa", rgb: "rgb(96, 165, 250)" },
      { name: "blue-500", hex: "#3b82f6", rgb: "rgb(59, 130, 246)" },
      { name: "blue-600", hex: "#2563eb", rgb: "rgb(37, 99, 235)" },
      { name: "blue-700", hex: "#1d4ed8", rgb: "rgb(29, 78, 216)" },
      { name: "blue-800", hex: "#1e40af", rgb: "rgb(30, 64, 175)" },
      { name: "blue-900", hex: "#1e3a8a", rgb: "rgb(30, 58, 138)" },
    ],
  },
  {
    name: "Purple",
    colors: [
      { name: "purple-50", hex: "#f5f3ff", rgb: "rgb(245, 243, 255)" },
      { name: "purple-100", hex: "#ede9fe", rgb: "rgb(237, 233, 254)" },
      { name: "purple-200", hex: "#ddd6fe", rgb: "rgb(221, 214, 254)" },
      { name: "purple-300", hex: "#c4b5fd", rgb: "rgb(196, 181, 253)" },
      { name: "purple-400", hex: "#a78bfa", rgb: "rgb(167, 139, 250)" },
      { name: "purple-500", hex: "#8b5cf6", rgb: "rgb(139, 92, 246)" },
      { name: "purple-600", hex: "#7c3aed", rgb: "rgb(124, 58, 237)" },
      { name: "purple-700", hex: "#6d28d9", rgb: "rgb(109, 40, 217)" },
      { name: "purple-800", hex: "#5b21b6", rgb: "rgb(91, 33, 182)" },
      { name: "purple-900", hex: "#4c1d95", rgb: "rgb(76, 29, 149)" },
    ],
  },
];

const muiColors: ColorGroup[] = [
  {
    name: "Blue",
    colors: [
      { name: "blue-50", hex: "#e3f2fd", rgb: "rgb(227, 242, 253)" },
      { name: "blue-100", hex: "#bbdefb", rgb: "rgb(187, 222, 251)" },
      { name: "blue-200", hex: "#90caf9", rgb: "rgb(144, 202, 249)" },
      { name: "blue-300", hex: "#64b5f6", rgb: "rgb(100, 181, 246)" },
      { name: "blue-400", hex: "#42a5f5", rgb: "rgb(66, 165, 245)" },
      { name: "blue-500", hex: "#2196f3", rgb: "rgb(33, 150, 243)" },
      { name: "blue-600", hex: "#1e88e5", rgb: "rgb(30, 136, 229)" },
      { name: "blue-700", hex: "#1976d2", rgb: "rgb(25, 118, 210)" },
      { name: "blue-800", hex: "#1565c0", rgb: "rgb(21, 101, 192)" },
      { name: "blue-900", hex: "#0d47a1", rgb: "rgb(13, 71, 161)" },
    ],
  },
  {
    name: "Purple",
    colors: [
      { name: "purple-50", hex: "#f3e5f5", rgb: "rgb(243, 229, 245)" },
      { name: "purple-100", hex: "#e1bee7", rgb: "rgb(225, 190, 231)" },
      { name: "purple-200", hex: "#ce93d8", rgb: "rgb(206, 147, 216)" },
      { name: "purple-300", hex: "#ba68c8", rgb: "rgb(186, 104, 200)" },
      { name: "purple-400", hex: "#ab47bc", rgb: "rgb(171, 71, 188)" },
      { name: "purple-500", hex: "#9c27b0", rgb: "rgb(156, 39, 176)" },
      { name: "purple-600", hex: "#8e24aa", rgb: "rgb(142, 36, 170)" },
      { name: "purple-700", hex: "#7b1fa2", rgb: "rgb(123, 31, 162)" },
      { name: "purple-800", hex: "#6a1b9a", rgb: "rgb(106, 27, 154)" },
      { name: "purple-900", hex: "#4a148c", rgb: "rgb(74, 20, 140)" },
    ],
  },
];

const radixColors: ColorGroup[] = [
  {
    name: "Blue",
    colors: [
      { name: "blue-1", hex: "#fbfdff", rgb: "rgb(251, 253, 255)" },
      { name: "blue-2", hex: "#f5faff", rgb: "rgb(245, 250, 255)" },
      { name: "blue-3", hex: "#edf6ff", rgb: "rgb(237, 246, 255)" },
      { name: "blue-4", hex: "#e1f0ff", rgb: "rgb(225, 240, 255)" },
      { name: "blue-5", hex: "#cee7fe", rgb: "rgb(206, 231, 254)" },
      { name: "blue-6", hex: "#b7d9f8", rgb: "rgb(183, 217, 248)" },
      { name: "blue-7", hex: "#96c7f2", rgb: "rgb(150, 199, 242)" },
      { name: "blue-8", hex: "#5eb0ef", rgb: "rgb(94, 176, 239)" },
      { name: "blue-9", hex: "#0091ff", rgb: "rgb(0, 145, 255)" },
      { name: "blue-10", hex: "#0081f1", rgb: "rgb(0, 129, 241)" },
    ],
  },
  {
    name: "Purple",
    colors: [
      { name: "purple-1", hex: "#fefcfe", rgb: "rgb(254, 252, 254)" },
      { name: "purple-2", hex: "#fbf8ff", rgb: "rgb(251, 248, 255)" },
      { name: "purple-3", hex: "#f7f2ff", rgb: "rgb(247, 242, 255)" },
      { name: "purple-4", hex: "#f1eaff", rgb: "rgb(241, 234, 255)" },
      { name: "purple-5", hex: "#e9deff", rgb: "rgb(233, 222, 255)" },
      { name: "purple-6", hex: "#deccff", rgb: "rgb(222, 204, 255)" },
      { name: "purple-7", hex: "#cfb1ff", rgb: "rgb(207, 177, 255)" },
      { name: "purple-8", hex: "#bd8df9", rgb: "rgb(189, 141, 249)" },
      { name: "purple-9", hex: "#9d5cee", rgb: "rgb(157, 92, 238)" },
      { name: "purple-10", hex: "#8e4ec6", rgb: "rgb(142, 78, 198)" },
    ],
  },
];

const getPaletteColors = () => {
  if (selectedPalette.value === "tailwind") {
    return tailwindColors;
  } else if (selectedPalette.value === "mui") {
    return muiColors;
  } else {
    return radixColors;
  }
};

const currentPaletteColors = computed(() => getPaletteColors());

const startDemo = () => {
  demoActive.value = true;
};

const stopDemo = () => {
  demoActive.value = false;
  selectedColor.value = null;
  showCopied.value = false;
};

const selectColor = (color: ColorOption) => {
  selectedColor.value = color;
  hoveredColor.value = null;
};

const copyColorFormat = (format: string) => {
  if (!selectedColor.value) return;

  copiedFormat.value = format;
  showCopied.value = true;

  // Hide copied message after 2 seconds
  setTimeout(() => {
    showCopied.value = false;
  }, 2000);
};
</script>

<style scoped>
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
</style>
