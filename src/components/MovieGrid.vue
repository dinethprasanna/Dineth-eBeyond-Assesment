<script setup>
import { ref, onMounted } from 'vue';
import MovieCard from '@/components/MovieCard.vue';

import { defineProps } from 'vue';

import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
    gsap.from(".movie-grid .mov-section-header", {
        y: 200,
        opacity: 0.5,
        duration: 0.6,
        ease: "ease",
        scrollTrigger: {
            trigger: ".movie-grid",
            start: "top 88%",
            end: "top 82%",
        }
    });

    gsap.from(".movie-grid .movie_cards_grid ", {
        y: 100,
        scale: 0.8,
        opacity: 0.5,
        duration: 1,
        ease: "ease",
        scrollTrigger: {
            trigger: ".movie-grid .mov-section-header",
            start: "top 90%",
            end: "top 80%",
        }
    });
});

defineProps({
    title: {
        type: String,
        default: 'Collect your favourites',
    },
    search_box_text: {
        type: String,
        default: 'Search title and add to grid',
    },
});


const defaultMovies = ref([]);
const addedMovies = ref([]);
const searchQuery = ref('');
const searchResults = ref([]);

const fetchDefaultMovies = async () => {
    try {
        const res = await fetch('https://api.tvmaze.com/shows');
        const data = await res.json();
        // console.log("data = ", data);
        defaultMovies.value = data.slice(0, 3); // First 3 shows
    } catch (err) {
        console.error('Failed to fetch default movies:', err);
    }
};

const handleSearch = async (e) => {
    e.preventDefault();
    if (!searchQuery.value) return;

    try {
        const res = await fetch(`https://api.tvmaze.com/search/shows?q=${searchQuery.value}`);
        const data = await res.json();
        // console.log("data = ", data);
        searchResults.value = data.map(result => result.show);
    } catch (err) {
        console.error('Search failed:', err);
    }
};

const addToGrid = (movie) => {
    if (!addedMovies.value.find(m => m.id === movie.id)) {
        addedMovies.value.push(movie);
    }
};

const removeFromGrid = (id) => {
    defaultMovies.value = defaultMovies.value.filter(m => m.id !== id);
    addedMovies.value = addedMovies.value.filter(m => m.id !== id);
};

onMounted(() => {
    fetchDefaultMovies();
});
</script>

<template>
    <section class="movie-grid w-full bg-[#1c1c1c] py-8 md:py-10 lg:py-12 px-6 md:px-12 lg:px-4">
        <!-- Header -->
        <div
            class="mov-section-header max-w-[1280px] mx-auto border-b border-white mb-8 px-4 flex flex-col md:flex-row items-center justify-between gap-4">
            <h2 class="text-left w-full md:w-auto text-2xl font-medium text-white sm:text-3xl md:text-4xl mb-2 md:mb-6">
                {{ title }}</h2>

            <!-- Search Form -->
            <div
                class="search-form flex items-center bg-[#1c1c1c] border border-white rounded-md mb-4 md:mb-0 w-full md:w-auto">
                <form class="w-full" @submit="handleSearch">
                    <div class="relative text-white">
                        <span class="absolute inset-y-0 left-0 flex items-center pl-2">
                            <button type="submit" class="p-1 focus:outline-none focus:shadow-outline">
                                <svg xmlns="http://www.w3.org/2000/svg" width="22.414" height="22.414"
                                    viewBox="0 0 22.414 22.414">
                                    <g id="Icon_feather-search" data-name="Icon feather-search"
                                        transform="translate(1 1)">
                                        <path id="Path_17" data-name="Path 17"
                                            d="M22.278,13.389A8.889,8.889,0,1,1,13.389,4.5a8.889,8.889,0,0,1,8.889,8.889Z"
                                            transform="translate(-4.5 -4.5)" fill="none" stroke="#fff"
                                            stroke-linecap="round" stroke-linejoin="round" stroke-width="2" />
                                        <path id="Path_18" data-name="Path 18" d="M29.808,29.808l-4.833-4.833"
                                            transform="translate(-9.808 -9.808)" fill="none" stroke="#fff"
                                            stroke-linecap="round" stroke-linejoin="round" stroke-width="2" />
                                    </g>
                                </svg>

                            </button>
                        </span>
                        <input type="search" v-model="searchQuery" placeholder="Search title and add to grid"
                            class="py-2 w-[100%] text-base md:w-[400px] md:text-xl text-white rounded-md pl-10 focus:outline-none" />
                    </div>
                </form>
            </div>




        </div>

        <!-- Search Results -->
        <div v-if="searchQuery && searchResults.length"
            class="movie_cards_grid max-w-[1280px] mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mb-8">
            <MovieCard v-for="movie in searchResults" :key="movie.id" :movie="movie" :canAdd="true" @add="addToGrid" />
        </div>

        <!-- Main Grid -->
        <div v-if="!searchQuery"
            class="movie_cards_grid  max-w-[1280px] mx-auto grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
            <MovieCard v-for="movie in [...defaultMovies, ...addedMovies]" :key="movie.id" :movie="movie"
                :canClose="true" @close="removeFromGrid" />
        </div>
    </section>
</template>
