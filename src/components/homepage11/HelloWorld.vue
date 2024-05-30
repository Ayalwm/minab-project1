<template>
  <div class="flex pt-10">
    <!-- Carousel Component -->
    <div class="w-1/2 p-20">
      <h1 class="text-5xl pl-2 text-red-550">Ricky and Morty</h1>
      <carouselSwiper />
    </div>

    <!-- Story Genre Component -->
    <div class="w-1/2 pl-6">
      <storyGenre />
    </div>
  </div>
  <div class="bg-white min-h-screen">
    <!-- Top Navbar -->
    <SidebarNavigation @scrollTo="scrollToComponent" />

    <!-- Main Content -->
    <div class="pt-20 p-6">
      <div ref="episodes" class="mb-12 p-10">
        <Episodes />
      </div>
      <div ref="characters" class="mb-12 p-10">
        <Characters />
      </div>
      <div ref="locations">
        <Locations />
      </div>
    </div>
  </div>
  <footer class="bg-gray-400 text-white p-4 text-center mt-auto">
    <div class="flex justify-center space-x-4">
      <a
        href="https://www.figma.com/proto/yITCFDrpTUanCaydCbzd4a/ayal-figma?node-id=1-2&t=2sNdw97YnghZX2tU-1&scaling=scale-down&page-id=0%3A1&starting-point-node-id=1%3A2"
        target="_blank"
        rel="noopener noreferrer"
        class="text-pink-400"
        >Figma</a
      >
      <a
        href="https://github.com/ayalwm"
        target="_blank"
        rel="noopener noreferrer"
        class="text-gray-700"
        >GitHub</a
      >
    </div>
    <p>&copy; 2024 Ricky and Morty.</p>
  </footer>
</template>

<script setup>
import { ref } from "vue";
import SidebarNavigation from "./SidebarNavigation.vue";
import Episodes from "./episodeview.vue";
import Characters from "./CharacterView.vue";
import Locations from "./LocationView.vue";
import carouselSwiper from "../carouselSwiper.vue";
import storyGenre from "./storyGenre.vue";

const episodes = ref(null);
const characters = ref(null);
const locations = ref(null);

const scrollToComponent = (component) => {
  if (component === "episodes" && episodes.value) {
    episodes.value.scrollIntoView({ behavior: "smooth", block: "start" });
  } else if (component === "characters" && characters.value) {
    characters.value.scrollIntoView({ behavior: "smooth", block: "start" });
  } else if (component === "locations" && locations.value) {
    locations.value.scrollIntoView({ behavior: "smooth", block: "start" });
  }
};
</script>

<style scoped>
/* Add custom styles as needed */
</style>
