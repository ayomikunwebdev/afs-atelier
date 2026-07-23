<script setup>
const steps = [
  { number: '01', title: 'Consultation', description: 'Booking a session, discussing design silhouettes and fabrics.' },
  { number: '02', title: 'Materials', description: 'Hand-selecting luxurious silks, authentic Aṣọ-Òkè, laces, or premium wools.' },
  { number: '03', title: 'Fittings', description: "Precise geometric calibration to the client's body shape." },
  { number: '04', title: 'Delivery', description: 'Hand-finished, perfectly pressed garment ready for the occasion.' },
]

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
  <section id="process" ref="sectionRef" class="bg-black text-white py-20 px-6">
    <h2 class="text-3xl font-serif text-center mb-14">The Atelier Process</h2>

    <div class="grid grid-cols-1 md:grid-cols-4 gap-10 max-w-6xl mx-auto">
      <div
        v-for="step in steps"
        :key="step.number"
        class="text-center"
      >
        <p class="text-yellow-500 text-2xl font-serif mb-3">{{ step.number }}</p>
        <h3 class="text-lg uppercase tracking-wider mb-2">{{ step.title }}</h3>
        <p class="text-sm text-gray-400 leading-relaxed">{{ step.description }}</p>
      </div>
    </div>
  </section>
</template>