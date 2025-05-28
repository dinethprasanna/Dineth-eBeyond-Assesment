<script setup>
import { defineProps, defineEmits } from 'vue';
import card_close_icon from '@/assets/Icons/Close White.svg';
import card_add_icon from '@/assets/Icons/Add.png';

const props = defineProps({
  movie: Object,
  canClose: Boolean,
  canAdd: Boolean,
});

const emit = defineEmits(['close', 'add']);
</script>

<template>
  <div class="movie-card relative bg-[#2b2b2b] rounded-md overflow-hidden">

    <div v-if="canClose" class="absolute right-2 top-2 cursor-pointer z-10 p-4 bg-[#1c1c1c]" @click="$emit('close', movie.id)">
      <img :src="card_close_icon" alt="close" class="w-[16px] h-[16px] opacity-60 " />
    </div>
    <div v-if="canAdd" class="absolute right-2 top-2 cursor-pointer z-10" @click="$emit('add', movie)">
      <img :src="card_add_icon" alt="add" class="w-[32px] h-[32px] bg-green-900 rounded-full" />
    </div>

    <div class="card-img">
      <img :src="movie.image?.medium || 'https://via.placeholder.com/210x295?text=No+Image'" alt="" class="w-full h-[400px] object-cover" />
    </div>

    <div class="card-text-cont p-4">
      <h3 class="text-2xl text-white font-semibold mb-2">{{ movie.name }}</h3>
      <p class="text-white text-base line-clamp-3" v-html="movie.summary || 'No summary available.'"></p>
    </div>
  </div>
</template>
