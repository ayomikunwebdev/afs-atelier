<script setup>
import bookingImg from '../assets/images/booking/booking.jpg'
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
  <section id="booking" ref="sectionRef" class="bg-black text-white py-24 px-6 border-t border-gray-800">
    <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-12 items-center">

      <!-- Text side -->
      <div>
        <p class="text-xs tracking-widest text-gray-500 mb-4">CONTACT</p>
        <h2 class="text-4xl md:text-5xl font-serif mb-6">
          Place your order.
        </h2>
        <p class="text-gray-400 leading-relaxed mb-8 max-w-md">
          Reach the atelier directly. We respond within twenty-four hours, every day.
          Bring your event date, your fabric preferences, and the silhouette you have in mind.
        </p>

        <!-- WhatsApp + email -->
        <div class="flex flex-wrap items-center gap-6 mb-12">
        <a
          href="https://wa.me/2349067942501"
            target="_blank"
            class="bg-yellow-500 text-black px-6 py-3 rounded-full text-sm font-medium hover:bg-yellow-400 transition"
          >
            Chat on WhatsApp
          </a>
          <a
            href="mailto:Kasaliraimotabiodun@gmail.com"
            class="text-sm text-gray-300 hover:text-yellow-500 transition"
            >
            Kasaliraimotabiodun@gmail.com
          </a>
        </div>

        <!-- Studio info -->
        <div>
          <p class="text-xs tracking-widest text-gray-500 mb-3">STUDIO</p>
          <p class="font-medium mb-1">AFS — Abbey Fashion Stitches</p>
          <p class="text-gray-400 text-sm">Abeokuta, Ogun State</p>
          <p class="text-gray-400 text-sm mb-3">By appointment only</p>
          <a href="tel:+2349067942501" class="text-sm text-gray-300 hover:text-yellow-500 transition">
            +234 906 794 2501
          </a>
        </div>
      </div>

      <!-- Image side -->
      <img :src="bookingImg" alt="AFS Atelier" class="aspect-[4/5] w-full object-cover" />

    </div>
  </section>
</template>