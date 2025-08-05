<template>
  <section id="install" class="py-20 relative overflow-hidden">
    <!-- Background gradient elements -->
    <div class="absolute -top-40 -right-40 w-96 h-96 bg-indigo-200 rounded-full opacity-20 blur-3xl"></div>
    <div class="absolute -bottom-40 -left-40 w-96 h-96 bg-violet-200 rounded-full opacity-20 blur-3xl"></div>

    <div class="container mx-auto px-4 relative z-10">
      <div class="max-w-3xl mx-auto text-center">
        <h2 class="heading-secondary mb-6">Ready to Enhance Your Development Workflow?</h2>
        <p class="subtitle mb-10">Access colors instantly and speed up your design process with ColorLift.</p>

        <div class="flex flex-col md:flex-row gap-6 items-center justify-center">
          <div class="flex items-center text-gray-500">
            <Star class="h-4 w-4 text-amber-400" />
            <Star class="h-4 w-4 text-amber-400" />
            <Star class="h-4 w-4 text-amber-400" />
            <Star class="h-4 w-4 text-amber-400" />
            <Star class="h-4 w-4 text-amber-400" />
            <span class="ml-2 text-sm">Rated 4.9/5 from 200+ users</span>
          </div>
        </div>

        <div class="mt-16 border border-gray-200 rounded-lg p-6 bg-white/50 backdrop-blur-sm">
          <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
            <div>
              <div class="text-4xl font-bold text-indigo-600 mb-2">400+</div>
              <p class="text-gray-600">Colors available</p>
            </div>
            <div>
              <div class="text-4xl font-bold text-indigo-600 mb-2">5+</div>
              <p class="text-gray-600">Design systems</p>
            </div>
            <div>
              <div class="text-4xl font-bold text-indigo-600 mb-2">100%</div>
              <p class="text-gray-600">Free to use</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Star } from "lucide-vue-next";
</script>
