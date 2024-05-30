<template>
  <div class="fixed top-0 left-0 right-0 z-50 p-4 bg-white shadow-md">
    <router-link :to="{ name: 'home' }">Home</router-link>
  </div>
  <div class="flex h-screen bg-white">
    <!-- Sidebar with character info -->
    <div class="flex-shrink-0 flex flex-col justify-center ml-6 bg-white">
      <div v-if="character">
        <div class="text-center">
          <img
            :src="character.image"
            alt=""
            class="w-56 h-56 object-cover rounded-lg mx-auto mb-4" />
          <h2 class="text-xl font-semibold text-gray-700">
            {{ character.name }}
          </h2>
          <p class="text-gray-600">Species: {{ character.species }}</p>
          <p class="text-gray-600">Gender: {{ character.gender }}</p>
          <p class="text-gray-600">
            Last Known Location: {{ character.location.name }}
          </p>
        </div>
      </div>
    </div>
    <!-- Main content area -->
    <div class="flex-grow overflow-y-auto p-6">
      <h1 class="text-2xl font-bold text-gray-800 mb-6">Character Details</h1>
      <div v-if="loading" class="text-lg text-gray-600">Loading...</div>
      <div v-if="error" class="text-lg text-red-600">
        Error: {{ error.message }}
      </div>
      <template v-if="character">
        <div class="mt-8">
          <h3 class="text-2xl font-bold text-gray-800 mb-6">
            {{ character.name }} participated Episodes
          </h3>
          <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
            <div
              v-for="episode in character.episode"
              :key="episode.id"
              class="bg-white border border-gray-200 rounded-lg p-4 shadow-md">
              <h4 class="text-lg font-semibold text-gray-700">
                {{ episode.name }}
              </h4>
              <p class="text-gray-600">Air Date: {{ episode.air_date }}</p>
              <p class="text-gray-600">Episode: {{ episode.episode }}</p>
              <p class="text-gray-600">Created: {{ episode.created }}</p>
            </div>
          </div>
        </div>
      </template>
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
const CHARACTER_QUERY = gql`
  query Character($id: ID!) {
    character(id: $id) {
      id
      name
      species
      gender
      image
      location {
        name
      }
      episode {
        id
        name
        air_date
        episode
        created
      }
    }
  }
`;

export default {
  name: "CharacterDetail",
  setup() {
    const route = useRoute();
    const { result, loading, error } = useQuery(CHARACTER_QUERY, {
      id: route.params.id,
    });
    const character = ref(null);

    watchEffect(() => {
      if (result.value) {
        character.value = result.value.character;
      }
    });

    return {
      character,
      loading,
      error,
    };
  },
};
</script>

<style scoped>
.grid {
  display: grid;
  gap: 1.5rem;
}
</style>
