<script setup>
import { ref, computed, onMounted, watch, useTemplateRef } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

// This automatically grabs EVERY image inside the lookbook folder at once
const imageModules = import.meta.glob('../assets/images/lookbook/*.{jpg,jpeg,png}', { eager: true })

// This maps a filename's starting word to a real category name
const categoryMap = {
  'aso-ebi': 'Aso Ebi',
  bridal: 'Bridal',
  cooperatew: 'Corporate',
  graduation: 'Graduation',
  evening: 'Evening',
}

const outfits = ref(
  Object.entries(imageModules)
    .map(([path, mod], index) => {
      const filename = path.split('/').pop() // e.g. "bridal-1.jpg"
      const prefixKey = Object.keys(categoryMap).find(key => filename.startsWith(key))
      const category = categoryMap[prefixKey] || 'Other'

      // Pull just the number out of the filename, e.g. "3" from "bridal-3.jpg"
      const numberMatch = filename.match(/(\d+)/)
      const number = numberMatch ? numberMatch[1] : ''

      return {
        id: index,
        title: `${category} Style ${number}`,
        category,
        image: mod.default,
      }
    })
    .sort((a, b) => a.title.localeCompare(b.title, undefined, { numeric: true }))
)

const activeFilter = ref('All')
const categories = ['All', 'Bridal', 'Aso Ebi', 'Corporate', 'Graduation', 'Evening']

const filteredOutfits = computed(() => {
  if (activeFilter.value === 'All') return outfits.value
  return outfits.value.filter(outfit => outfit.category === activeFilter.value)
})

// Whenever the filter changes, tell GSAP to recalculate section positions
watch(activeFilter, () => {
  setTimeout(() => {
    ScrollTrigger.refresh()
  }, 100)
})


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

// Tracks which outfit is currently selected for the detail view (null = none open)
const selectedOutfit = ref(null)

// Builds a WhatsApp link that includes the outfit name in the message automatically
function whatsappLink(outfit) {
  const message = `Hi, I'm interested in the "${outfit.title}" style. Can you tell me more?`
  return `https://wa.me/2349067942501?text=${encodeURIComponent(message)}`
}
</script>

<template>
  <section id="lookbook" ref="sectionRef" class="bg-black text-white py-20 px-6">
    <h2 class="text-3xl font-serif text-center mb-10">The Lookbook</h2>

    <!-- Filter buttons -->
    <div class="flex flex-wrap justify-center gap-4 mb-12">
      <button
        v-for="cat in categories"
        :key="cat"
        @click="activeFilter = cat"
        :class="[
          'px-4 py-2 text-sm uppercase tracking-wider rounded-full border transition',
          activeFilter === cat
            ? 'bg-yellow-500 text-black border-yellow-500'
            : 'border-white text-white hover:border-yellow-500 hover:text-yellow-500'
        ]"
      >
        {{ cat }}
      </button>
    </div>

    <!-- Gallery grid -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-6xl mx-auto">
      <div
        v-for="outfit in filteredOutfits"
        :key="outfit.id"
        @click="selectedOutfit = outfit"
        class="aspect-[3/4] overflow-hidden hover:scale-105 transition cursor-pointer"
      >
       <img :src="outfit.image" :alt="outfit.title" class="w-full h-full object-cover object-top" />
      </div>
       <!-- Detail popup -->
    <Teleport to="body">
      <div
        v-if="selectedOutfit"
        @click="selectedOutfit = null"
        class="fixed inset-0 bg-black/80 flex items-center justify-center z-50 p-6"
      >
        <div
          @click.stop
          class="bg-black border border-gray-800 max-w-2xl w-full grid grid-cols-1 md:grid-cols-2 gap-6 p-6"
        >
          <img :src="selectedOutfit.image" :alt="selectedOutfit.title" class="w-full aspect-[3/4] object-cover" />

          <div class="flex flex-col justify-center">
            <p class="text-xs tracking-widest text-gray-500 mb-2">{{ selectedOutfit.category }}</p>
            <h3 class="text-2xl font-serif mb-3">{{ selectedOutfit.title }}</h3>
            <p class="text-yellow-500 mb-6">Price on request</p>

            <a
              :href="whatsappLink(selectedOutfit)"
              target="_blank"
              class="bg-yellow-500 text-black text-center px-6 py-3 rounded-full font-medium hover:bg-yellow-400 transition"
            >
              Order This Style
            </a>

            <button
              @click="selectedOutfit = null"
              class="text-sm text-gray-400 mt-4 hover:text-white transition"
            >
              Close
            </button>
          </div>
        </div>
      </div>
    </Teleport>
    </div>
  </section>
</template>