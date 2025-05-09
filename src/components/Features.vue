<template>
  <section id="features" class="py-20 bg-gray-50">
    <div class="container mx-auto px-4">
      <div class="text-center max-w-3xl mx-auto mb-16">
        <h2 class="heading-secondary">Features that make color selection a breeze</h2>
        <p class="subtitle">ColorLift streamlines your workflow with easy access to popular color systems</p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div
          v-for="(feature, index) in features"
          :key="index"
          class="bg-white p-8 rounded-xl shadow-sm hover:shadow-md transition-all duration-300 border border-gray-100"
        >
          <div class="w-12 h-12 rounded-lg flex items-center justify-center mb-5" :class="feature.bgColor">
            <component :is="feature.icon" class="h-6 w-6 text-white" />
          </div>
          <h3 class="text-xl font-semibold mb-3">{{ feature.title }}</h3>
          <p class="text-gray-600">{{ feature.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Palette, Copy, Zap, Search, Github, Figma } from "lucide-vue-next";

const features = [
  {
    title: "Popular Design Systems",
    description:
      "Access colors from Material UI, Tailwind CSS, Radix (light & dark), with more systems coming soon through community contributions.",
    icon: Palette,
    bgColor: "bg-indigo-600",
  },
  {
    title: "Multiple Color Formats",
    description: "Copy colors in HEX and RGB formats with a single click. Perfect for both code and design tools.",
    icon: Copy,
    bgColor: "bg-violet-600",
  },
  {
    title: "Lightning Fast Access",
    description:
      "Open the color picker instantly and get what you need without disrupting your workflow in VS Code, Figma, or any other tool.",
    icon: Zap,
    bgColor: "bg-blue-600",
  },
  {
    title: "Smart Search",
    description: "Quickly find colors by name or value across all available design systems.",
    icon: Search,
    bgColor: "bg-pink-600",
  },
  {
    title: "Open Source",
    description:
      "Contribute new features, suggest improvements, or add support for your favorite design system through our GitHub repository.",
    icon: Github,
    bgColor: "bg-emerald-600",
  },
  {
    title: "Design Tool Ready",
    description: "Seamlessly use ColorLift with Figma and other design tools to maintain consistency across your projects.",
    icon: Figma,
    bgColor: "bg-amber-600",
  },
];
</script>
