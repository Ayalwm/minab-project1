<template>
  <div class="fixed top-0 left-0 right-0 z-50 p-4 bg-white shadow-md">
    <router-link :to="{ name: 'home' }">Home</router-link>
  </div>
  <div class="flex h-screen bg-white">
    <!-- Fixed sidebar with episode details -->
    <div
      class="fixed left-0 top-0 bottom-0 z-40 w-64 p-6 bg-white overflow-y-auto flex flex-col justify-center">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">
        {{ episode.episode }}
      </h1>
      <div v-if="loading" class="text-lg text-gray-600">Loading...</div>
      <div v-if="error" class="text-lg text-red-600">
        Error: {{ error.message }}
      </div>
      <div v-if="episode">
        <h1 class="text-xl font-semibold text-gray-700">{{ episode.name }}</h1>
        <p class="text-gray-600">Air Date: {{ episode.air_date }}</p>
        <p class="text-gray-600">Created: {{ episode.created }}</p>
      </div>
    </div>

    <!-- Main content area -->
    <div class="flex-grow p-6 bg-white ml-64">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">Characters</h1>

      <h1 class="text-2xl font-bold text-gray-800 mb-6">
        Participated Characters
      </h1>
      <div v-if="loading" class="text-lg text-gray-600">Loading...</div>
      <div v-if="error" class="text-lg text-red-600">
        Error: {{ error.message }}
      </div>
      <div v-if="episode">
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
          <div
            v-for="character in episode.characters"
            :key="character.id"
            class="bg-white border border-gray-200 rounded-lg p-4 shadow-md flex flex-col items-center relative overflow-hidden">
            <div class="relative w-full h-52">
              <img
                :src="character.image"
                alt=""
                class="w-full h-full rounded-lg cursor-pointer transition-opacity duration-300 hover:opacity-80 hover:bg-gray-200" />
              <div
                class="absolute bottom-0 left-0 bg-gray-800 bg-opacity-70 rounded-br-lg rounded-tr-lg p-2 text-left text-gray-200">
                <p class="text-lg font-semibold">{{ character.name }}</p>
                <p class="text-sm">Species: {{ character.species }}</p>
                <p class="text-sm">Status: {{ character.status }}</p>
                <p class="text-sm">Gender: {{ character.gender }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <footer
    class="fixed bottom-0 left-0 right-0 z-50 bg-gray-400 text-white p-4 text-center">
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

<script>
import { ref, watchEffect } from "vue";
import gql from "graphql-tag";
import { useQuery } from "@vue/apollo-composable";
import { useRoute } from "vue-router";

const EPISODE_QUERY = gql`
  query Episode($id: ID!) {
    episode(id: $id) {
      name
      air_date
      episode
      created
      characters {
        id
        name
        species
        status
        gender
        image
      }
    }
  }
`;

export default {
  name: "CharacterDetail",
  setup() {
    const route = useRoute();
    const { result, loading, error } = useQuery(EPISODE_QUERY, {
      id: route.params.id,
    });
    const episode = ref(null);

    watchEffect(() => {
      if (result.value) {
        episode.value = result.value.episode;
      }
    });

    return {
      episode,
      loading,
      error,
    };
  },
};
</script>

<style scoped>
.bg-white {
  background-color: #ffffff;
}
</style>
