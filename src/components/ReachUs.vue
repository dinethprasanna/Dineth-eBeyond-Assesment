<script setup>
import { defineProps, onMounted } from 'vue';
import ContactUsForm from '@/components/ContactUsForm.vue';
import MapLocation from '@/components/MapLocation.vue';

import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
    gsap.from(".reach-us .reach-us-header", {
        y: 200,
        opacity: 0.5,
        duration: 0.6,
        ease: "ease",
        scrollTrigger: {
            trigger: ".reach-us",
            start: "top 88%",
            end: "top 82%",
        }
    });

    gsap.from(".reach-us .contact-form-map ", {
        y: 100,
        scale: 0.8,
        opacity: 0.5,
        duration: 1,
        ease: "ease",
        scrollTrigger: {
            trigger: ".reach-us .reach-us-header",
            start: "top 90%",
            end: "top 80%",
        }
    });
});

defineProps({
    title: {
        type: String,
        default: 'How to reach us',
    },
    subtitle: {
        type: String,
        default: 'Lorem ipsum dolor sit amet, consetetur.',
    },
});
</script>

<template>
    <section class="reach-us max-w-[1280px] mx-auto pb-0 pt-8 md:pt-10 lg:pt-12 lg:pb-12 ">
        <div class="reach-us-header mb-8 md:mb-12 px-6 md:px-12 lg:px-4">
            <h2 class="text-2xl font-medium text-white sm:text-3xl md:text-4xl mb-6">{{ title }}</h2>
            <p class="my-4 w-[230px] md:w-full text-xl text-[#64889c] ">
                {{ subtitle }}
            </p>
        </div>

        <div class="contact-form-map flex flex-col lg:flex-row gap-12">
            <div class="w-full lg:w-[40%] px-6 md:px-12 lg:px-4">
                <ContactUsForm />
            </div>
            <div class="w-[100%] lg:w-[60%]">
                <MapLocation />
            </div>
        </div>

    </section>
</template>