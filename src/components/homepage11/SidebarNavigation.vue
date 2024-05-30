<template>
  <div class="fixed top-0 left-0 right-0 z-50 p-4 bg-white shadow-md">
    <div class="flex justify-between items-center">
      <router-link :to="{ name: 'home' }" class="text-gray-800"
        >Home</router-link
      >
      <div class="flex space-x-4">
        <a
          href="#"
          @click="scrollTo('episodes')"
          class="text-gray-800 hover:text-gray-600 cursor-pointer"
          >Episodes</a
        >
        <a
          href="#"
          @click="scrollTo('characters')"
          class="text-gray-800 hover:text-gray-600 cursor-pointer"
          >Characters</a
        >
        <a
          href="#"
          @click="scrollTo('locations')"
          class="text-gray-800 hover:text-gray-600 cursor-pointer"
          >Locations</a
        >
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineEmits } from "vue";

const emit = defineEmits(["scrollTo"]);

const scrollTo = (component) => {
  emit("scrollTo", component);
};
</script>

<style scoped>
/* Add custom styles as needed */
</style>
