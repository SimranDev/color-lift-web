<template>
  <section
    ref="heroSection"
    class="pt-42 pb-28 px-4 overflow-hidden relative"
    @mousemove="handleMouseMove"
    @mouseleave="resetTransform"
  >
    <!-- Background gradient elements -->
    <div class="absolute -top-24 -left-24 w-96 h-96 bg-indigo-200 rounded-full opacity-20 blur-3xl"></div>
    <div class="absolute -bottom-24 -right-24 w-96 h-96 bg-violet-200 rounded-full opacity-20 blur-3xl"></div>

    <div class="container mx-auto">
      <div class="flex flex-col lg:flex-row gap-12 items-center justify-center">
        <div class="flex-1 max-w-xl mx-auto text-center lg:text-left">
          <h1 class="heading-primary leading-14">
            Quick access to
            <span class="rainbow-text">color palettes</span> for everyone
          </h1>
          <p class="subtitle mt-6">
            Access popular design system colors like Material UI, Tailwind, and Radix directly in your browser. Perfect for
            developers and designers working with Figma, VS Code, or any design tool.
          </p>

          <div class="mt-8 flex items-center justify-center lg:justify-start text-gray-500 text-sm flex-wrap gap-4">
            <div
              class="flex items-center bg-gradient-to-r from-green-50 to-emerald-50 px-3 py-1 rounded-full border border-green-200"
            >
              <div class="flex items-center">
                <Code class="h-4 w-4 mr-2 text-green-500" />
                <span class="text-green-700 font-medium">Free & Open Source</span>
              </div>
            </div>

            <div
              class="flex items-center bg-gradient-to-r from-amber-50 to-yellow-50 px-3 py-1 rounded-full border border-amber-200"
            >
              <div class="flex items-center">
                <Award class="h-4 w-4 mr-2 text-amber-500" />
                <span class="text-amber-700 font-medium">Google Featured Badge</span>
              </div>
            </div>
          </div>
        </div>
        <!-- Screenshot-->
        <div ref="screenshotContainer" class="flex-1 relative mx-auto flex justify-center">
          <img
            ref="screenshotImg"
            src="/src/assets/screenshot.png"
            alt="Color Lift Extension Screenshot"
            class="w-auto h-auto max-h-[560px] rounded-lg transition-transform duration-300 ease-out screenshot-shadow"
            :style="imageTransform"
          />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Award, Code } from "lucide-vue-next";
import { ref, computed } from "vue";

const heroSection = ref<HTMLElement | null>(null);
const screenshotContainer = ref<HTMLElement | null>(null);
const screenshotImg = ref<HTMLElement | null>(null);
const mouseX = ref(0);
const mouseY = ref(0);

const imageTransform = computed(() => {
  const rotateX = (mouseY.value - 0.5) * 10; // Max 5 degrees rotation
  const rotateY = (0.5 - mouseX.value) * 10; // Max 5 degrees rotation
  const translateX = (mouseX.value - 0.5) * 20; // Max 10px movement
  const translateY = (mouseY.value - 0.5) * 20; // Max 10px movement

  return `transform: perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateX(${translateX}px) translateY(${translateY}px);`;
});

const handleMouseMove = (event: MouseEvent) => {
  if (!heroSection.value) return;

  const rect = heroSection.value.getBoundingClientRect();
  const centerX = rect.left + rect.width / 2;
  const centerY = rect.top + rect.height / 2;

  // Normalize mouse position to -0.5 to 0.5 range
  mouseX.value = (event.clientX - centerX) / rect.width;
  mouseY.value = (event.clientY - centerY) / rect.height;
};

const resetTransform = () => {
  mouseX.value = 0;
  mouseY.value = 0;
};
</script>

<style scoped>
.rainbow-text {
  background: linear-gradient(45deg, #ff0000, #ff7f00, #ffff00, #00ff00, #0000ff, #4b0082, #9400d3);
  background-size: 400% 400%;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: rainbowShift 12s ease-in-out infinite;
}

@keyframes rainbowShift {
  0%,
  100% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
}

.screenshot-shadow {
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.25), 0 0 0 1px rgba(255, 255, 255, 0.05), 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
}
</style>
