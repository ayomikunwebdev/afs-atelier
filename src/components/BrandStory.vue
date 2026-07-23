<script setup>
import aboutImg from '../assets/images/about/about.jpg'
import { onMounted, useTemplateRef } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = useTemplateRef('sectionRef')

onMounted(() => {
  gsap.from(sectionRef.value, {
    opacity: 0,
    y: 40,
    duration: 1.5,
    ease: 'power2.out',
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top 70%',
    },
  })
})
</script>

<template>
  <section id="about" ref="sectionRef" class="bg-black text-white py-24 px-6">
    <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-12 items-center">

      <!-- Image side -->
      <img :src="aboutImg" alt="AFS Atelier" class="aspect-[4/5] w-full object-cover" />

      <!-- Text side -->
      <div>
        <p class="text-xs tracking-widest text-gray-500 mb-4">THE ATELIER STORY</p>
        <h2 class="text-3xl md:text-4xl font-serif mb-6 leading-snug">
          Where heritage meets <span class="italic">elegance.</span>
        </h2>
        <p class="italic text-gray-400 mb-6">
          "Every stitch tells a story of identity, craft, and celebration."
        </p>
        <p class="text-gray-300 leading-relaxed">
          Rooted in Yoruba craftsmanship, AFS brings architectural precision to
          bridal, Aso Ebi, and corporate wear. Every garment is hand-finished,
          embedding cultural detail into timeless, modern silhouettes.
        </p>
      </div>

    </div>
  </section>
</template>