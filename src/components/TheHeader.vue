<script setup>
import { ref } from 'vue'

// Tracks whether the mobile menu is open or closed
const menuOpen = ref(false)
</script>

<template>
  <header class="bg-black text-white px-6 py-4 relative">
    <div class="flex items-center justify-between">
      <!-- Left: Brand logo -->
      <div class="leading-tight">
        <p class="text-xl font-serif italic tracking-wide">A F S</p>
        <p class="text-[10px] tracking-[0.25em] text-gray-400">ABBEY FASHION STITCHES</p>
      </div>

      <!-- Center: Nav links (desktop only) -->
      <nav class="hidden md:flex gap-8 text-sm uppercase tracking-wider">
        <a href="#lookbook" class="hover:text-yellow-500 transition">Collections</a>
        <a href="#about" class="hover:text-yellow-500 transition">About Us</a>
        <a href="#services" class="hover:text-yellow-500 transition">Our Services</a>
        <a href="#booking" class="hover:text-yellow-500 transition">Contact Us</a>
      </nav>

      <!-- Right side: WhatsApp button (desktop) + hamburger (mobile) -->
      <div class="flex items-center gap-4">
        <a
          href="https://wa.me/2349067942501"
          target="_blank"
          class="hidden md:inline-block bg-yellow-500 text-black text-sm px-4 py-2 rounded-full font-medium hover:bg-yellow-400 transition"
        >
          Order
        </a>

        <!-- Hamburger button (mobile only) -->
        <button
          @click="menuOpen = !menuOpen"
          class="md:hidden text-white text-2xl"
        >
          {{ menuOpen ? '✕' : '☰' }}
        </button>
      </div>
    </div>

    <!-- Mobile dropdown menu -->
    <div
      v-if="menuOpen"
      class="md:hidden flex flex-col gap-6 mt-6 pb-6 text-sm uppercase tracking-wider"
    >
      <a href="#lookbook" @click="menuOpen = false" class="hover:text-yellow-500 transition">Collections</a>
      <a href="#about" @click="menuOpen = false" class="hover:text-yellow-500 transition">About Us</a>
      <a href="#services" @click="menuOpen = false" class="hover:text-yellow-500 transition">Our Services</a>
      <a href="#booking" @click="menuOpen = false" class="hover:text-yellow-500 transition">Contact Us</a>
      <a
        href="https://wa.me/2349067942501"
        target="_blank"
        class="bg-yellow-500 text-black text-center px-4 py-2 rounded-full font-medium"
      >
        Order
      </a>
    </div>
  </header>
</template>