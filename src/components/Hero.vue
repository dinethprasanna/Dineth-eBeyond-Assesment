<script setup>
import { defineProps, onMounted } from 'vue';

import { gsap } from 'gsap';

onMounted(() => {
    gsap.from(".hero-image", {
        y: 100,
        duration: 1,
        ease: "ease",
        opacity: 0
    });

    gsap.from(".hero .hero-text-cont", {
        x: 100,
        duration: 1.5,
        ease: "elastic.out(1,0.3)",
    });
});

defineProps({
  title: {
    type: String,
    default: 'Heading Title',
  },
  subtitle: {
    type: String,
    default: 'Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.',
  },
});
</script>

<template>
  <section class="hero relative overflow-hidden pb-12">
    <div class="hero-image w-full border-b border-gray-900">

      <img src="@/assets/Images/Header Image.jpg" alt="Hero"
        class="hidden md:block w-full object-cover object-bottom h-[32vh] md:h-[30vh] lg:h-[80vh]" />

      <img src="@/assets/Images/Header Mob Image.jpg" alt="Hero"
        class="block md:hidden w-full object-cover object-bottom h-[90vw]" />
      
    </div>
    <div class="max-w-[1280px] mx-auto flex flex-col items-start px-6 md:px-12 lg:px-4">
      <div class="hero-text-cont text-left pt-12">
        <h1 class="text-3xl font-medium text-white sm:text-4xl md:text-5xl mb-6">
          {{ title }}
        </h1>
        <p class="my-4 text-xl text-[#64889c] max-w-[520px]">
          {{ subtitle }}
        </p>
      </div>
    </div>
  </section>
</template>