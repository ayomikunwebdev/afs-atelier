<script setup>
import bridalImg from '../assets/images/services/bridal.jpg'
import asoebiImg from '../assets/images/services/asoebi.jpg'
import corporateImg from '../assets/images/services/corporate.jpg'
import graduationImg from '../assets/images/services/graduation.jpg'
import eveningImg from '../assets/images/services/evening.jpg'

const services = [
  {
    title: 'Bridal Couture',
    description: 'Custom wedding gowns designed and tailored to your exact measurements and vision.',
    image: bridalImg,
  },
  {
    title: 'Aso Ebi Styling',
    description: 'Coordinated group designs for weddings, owambe, and traditional ceremonies.',
    image: asoebiImg,
  },
  {
    title: 'Corporate Wear',
    description: 'Sharp, structured office and formal wear tailored for the modern professional.',
    image: corporateImg,
  },
  {
    title: 'Graduation & Convocation',
    description: 'Elegant gowns and outfits designed for graduation and academic ceremonies.',
    image: graduationImg,
  },
  {
    title: 'Evening & Occasion Wear',
    description: 'Statement pieces crafted for galas, dinners, and special events.',
    image: eveningImg,
  },
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
  <section id="services" ref="sectionRef" class="bg-black text-white py-20 px-6">
    <h2 class="text-3xl font-serif text-center mb-14">Our Services</h2>

    <div class="grid grid-cols-1 md:grid-cols-3 gap-10 max-w-5xl mx-auto">
      <div
        v-for="service in services"
        :key="service.title"
        class="border border-gray-800 hover:border-yellow-500 transition overflow-hidden"
      >
        <img :src="service.image" :alt="service.title" class="w-full aspect-[3/4] object-cover" />
        <div class="p-6">
          <h3 class="text-lg uppercase tracking-wider mb-3">{{ service.title }}</h3>
          <p class="text-sm text-gray-400 leading-relaxed">{{ service.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>