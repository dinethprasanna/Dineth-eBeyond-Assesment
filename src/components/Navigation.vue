<script setup>
import { RouterLink, useRoute } from "vue-router";
import logo from '@/assets/Logos/Logo White.svg';
import hamburg_menu_icon from '@/assets/Icons/Menu White.svg';
import hamburg_menu_close_icon from '@/assets/Icons/Close White.svg';
import { ref, computed } from 'vue';

const isActivelink = (routePath) => {
    const route = useRoute();
    return route.path === routePath;
}

const isMenuOpen = ref(false);
const toggleMenu = () => {
    isMenuOpen.value = !isMenuOpen.value;
};
const currentIcon = computed(() => isMenuOpen.value ? hamburg_menu_close_icon : hamburg_menu_icon);
</script>

<template>
    <header class="px-2 md:px-2 lg:px-4 py-6 border-b border-gray-900">
        <nav class="max-w-[1280px] mx-auto flex flex-row justify-between items-center">
            <RouterLink to="/">
                <div class="logo max-w-[164px]"><img :src="logo" alt="Logo" width="100%" height="auto" /></div>
            </RouterLink>

            <div class="nav-links-area flex justify-between items-center relative">
                <ul class="link-list text-white gap-4 mr-6 hidden md:flex">
                    <li class="list-none">
                        <RouterLink to="/"
                            :class="[isActivelink('/') ? 'underline !text-white' : '', 'px-2 text-slate-300 block inline-block']">
                            HOME</RouterLink>
                    </li>
                    <li class="list-none">
                        <RouterLink to="/our-screen"
                            :class="[isActivelink('/our-screen') ? 'underline !text-white' : '', 'px-2 text-slate-300 block inline-block']">
                            OUR SCREENS</RouterLink>
                    </li>
                    <li class="list-none">
                        <RouterLink to="/schedule"
                            :class="[isActivelink('/schedule') ? 'underline !text-white' : '', 'px-2 text-slate-300 block inline-block']">
                            SCHEDULE</RouterLink>
                    </li>
                    <li class="list-none">
                        <RouterLink to="/movie-library"
                            :class="[isActivelink('/movie-library') ? 'underline !text-white' : '', 'px-2 text-slate-300 block inline-block']">
                            MOVIE LIBRARY</RouterLink>
                    </li>
                    <li class="list-none hidden lg:inline-block">
                        <RouterLink to="/location-and-contact"
                            :class="[isActivelink('/location-and-contact') ? 'underline !text-white' : '', 'px-2 text-slate-300 block inline-block']">
                            LOCATION & CONTACT</RouterLink>
                    </li>
                </ul>
                <div class="hamburg-menu-icon cursor-pointer" @click="toggleMenu">
                    <img :src="currentIcon" alt="Logo" width="100%" height="auto" class="w-[32px] " />
                </div>
                <div class="collapsed-menu-area transition-all duration-300 bg-black h-full lg:h-auto p-6 pr-3 lg:p-2 fixed z-12 right-0 top-0 lg:absolute lg:top-[54px] lg:right-[-8px] block"
                    :class="{ 'hidden': !isMenuOpen }">
                    <div class="menu-close text-white lg:hidden w-full " @click="toggleMenu"><img
                            :src="hamburg_menu_close_icon" alt="Close" width="100%" height="auto" class="w-[28px] ml-auto mt-2 mr-0 pb-2 mb-4" />
                    </div>
                    <div class="collapsed-menu">
                        <ul class="link-list text-white flex flex-col gap-12 lg:gap-4 mr-6">
                            <li class="list-none">
                                <RouterLink to="/gallery"
                                    :class="[isActivelink('/gallery') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    Gallery</RouterLink>
                            </li>
                            <li class="list-none block lg:hidden ">
                                <RouterLink to="/location-and-contact"
                                    :class="[isActivelink('/location-and-contact') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    LOCATION & CONTACT</RouterLink>
                            </li>
                            <li class="list-none block md:hidden">
                                <RouterLink to="/"
                                    :class="[isActivelink('/') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    HOME</RouterLink>
                            </li>
                            <li class="list-none block md:hidden">
                                <RouterLink to="/our-screen"
                                    :class="[isActivelink('/our-screen') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    OUR SCREENS</RouterLink>
                            </li>
                            <li class="list-none block md:hidden">
                                <RouterLink to="/schedule"
                                    :class="[isActivelink('/schedule') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    SCHEDULE</RouterLink>
                            </li>
                            <li class="list-none block md:hidden">
                                <RouterLink to="/movie-library"
                                    :class="[isActivelink('/movie-library') ? 'underline !text-white' : '', 'uppercase px-2 text-slate-300 block inline-block']">
                                    MOVIE LIBRARY</RouterLink>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

        </nav>
    </header>
</template>