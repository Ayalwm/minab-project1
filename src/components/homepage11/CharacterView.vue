<template>
  <h1 class="text-4xl">Some of the Characters:</h1>
  <div class="max-w-full mx-auto my-8 shadow-lg overflow-y-auto h-96">
    <div class="p-4">
      <div
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 lg:grid-cols-4 gap-8 pt-5">
        <router-link
          v-for="character in characters"
          :key="character.id"
          :to="{ name: 'CharacterDetail', params: { id: character.id } }"
          class="group text-center transform hover:scale-105 transition duration-300 ease-in-out">
          <div class="relative">
            <img
              :src="character.image"
              alt=""
              class="w-full h-full object-cover shadow-md group-hover:shadow-lg transition duration-300" />
            <div
              class="absolute inset-x-0 bottom-0 bg-gray-800 bg-opacity-80 py-2">
              <h2 class="text-lg font-semibold text-gray-200">
                {{ character.name }}
              </h2>
            </div>
          </div>
        </router-link>
      </div>
      <div v-if="characters.length === 0" class="text-gray-700 mt-4">
        No characters available.
      </div>
    </div>
  </div>
</template>

<script setup>
import gql from "graphql-tag";
import { ref, watch } from "vue";
import { useQuery } from "@vue/apollo-composable";

const CHARACTERS_QUERY = gql`
  query Characters {
    characters {
      results {
        id
        name
        image
      }
    }
  }
`;

const { result, loading, error, refetch } = useQuery(CHARACTERS_QUERY, null, {
  fetchPolicy: "network-only",
});
const characters = ref([]);

watch(result, (newResult) => {
  if (newResult && newResult.characters) {
    characters.value = newResult.characters.results;
  }
});

// Function to refetch characters
const fetchCharacters = async () => {
  await refetch();
  characters.value = result.value.characters.results;
};
</script>

<style scoped>
.group img {
  border-radius: 8px; /* Slightly round the corners of the image */
}

.grid {
  gap: 1.5rem;
}

.p-4 {
  padding: 1rem;
}

.text-lg {
  font-size: 1.125rem;
}
</style>
