<template>
  <section class="relative w-full h-screen overflow-hidden">
    <!-- Background video -->
    <video
      autoplay
      muted
      loop
      playsinline
      class="absolute inset-0 w-full h-full object-cover bg-black"
    >
      <source src="../assets/hero-video.mp4" type="video/mp4" />
    </video>

    <!-- Dark overlay -->
    <div class="absolute inset-0 bg-black/60"></div>

    <!-- Content -->
    <div class="relative z-10 flex flex-col justify-end h-full text-white px-6 md:px-16 pb-20">
      <p class="text-xs md:text-sm tracking-[0.3em] text-gray-300 mb-4">
        BESPOKE COUTURE · ABEOKUTA
      </p>

      <h1 class="text-4xl md:text-6xl font-serif leading-tight mb-6">
        Elegance,<br />
        <span class="italic">tailored perfectly.</span>
      </h1>

      <p class="text-sm md:text-base text-gray-300 max-w-md mb-8">
        Bespoke bridal, Aso Ebi, and corporate wear — hand-finished
        for every occasion that matters.
      </p>

      <a
        href="#lookbook"
        class="text-sm uppercase tracking-widest border-b border-white pb-1 w-fit hover:text-yellow-500 hover:border-yellow-500 transition"
      >
        Explore Collection
      </a>
    </div>

    <!-- Scroll hint -->
    <div class="absolute bottom-6 left-6 md:left-16 z-10 text-xs text-gray-400 tracking-widest">
      ↓ SCROLL
    </div>
  </section>
</template>