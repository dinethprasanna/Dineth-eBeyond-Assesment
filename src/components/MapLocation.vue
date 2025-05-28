<script setup>
import { defineProps } from 'vue';

defineProps({
    map_url: {
        type: String,
        default: '',
    },
});
</script>


<template>
    <div class="relative h-[60vh] lg:w-full lg:h-full">
        <iframe class="w-full h-full"
            src="https://www.google.com/maps/embed?pb=!1m14!1m8!1m3!1d20741986.601562705!2d-0.42020869339025596!3d39.0317443944846!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0xd422f35d4f0c269%3A0x754405946e8ca584!2sAmadeus%20IT%20Group!5e0!3m2!1sen!2slk!4v1748455153873!5m2!1sen!2slk"
            frameborder="0" style="border:0;" allowfullscreen="" aria-hidden="false" tabindex="0">
        </iframe>
    </div>
</template>