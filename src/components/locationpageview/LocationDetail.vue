<template>
  <div class="flex h-screen bg-gray-100">
    <!-- Location details -->
    <div class="flex-shrink-0 flex flex-col justify-center ml-6">
      <h2 class="text-xl font-semibold text-gray-700">{{ location.name }}</h2>
      <p class="text-gray-600">Type: {{ location.type }}</p>
      <p class="text-gray-600">Dimension: {{ location.dimension }}</p>
      <p class="text-gray-600">Created: {{ location.created }}</p>
    </div>
    <!-- Residents section -->
    <div class="flex-grow overflow-y-auto p-6 pt-20">
      <div class="fixed top-0 left-0 right-0 z-50 p-4 bg-white shadow-md">
        <router-link :to="{ name: 'home' }">Home</router-link>
      </div>

      <!-- Residents list -->
      <h1 class="m-2 text-2xl">Residents</h1>
      <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
        <div
          v-for="resident in location.residents"
          :key="resident.id"
          class="bg-white border border-gray-200 rounded-lg shadow-md p-4 hover:shadow-lg">
          <img
            :src="resident.image"
            alt=""
            class="w-24 h-24 rounded-full mb-2" />
          <div class="text-center">
            <p class="text-lg font-semibold text-gray-800">
              {{ resident.name }}
            </p>
            <p class="text-gray-600">Status: {{ resident.status }}</p>
            <p class="text-gray-600">Species: {{ resident.species }}</p>
            <p class="text-gray-600">Gender: {{ resident.gender }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
  <footer
    class="fixed bottom-0 left-0 right-0 z-50 bg-gray-400 text-white p-4 text-center">
    <div class="flex justify-center space-x-4">
      <a
        href="https://www.figma.com/proto/yITCFDrpTUanCaydCbzd4a?node-id=0-1&t=CGvh5FtAOa4EyhHs-6"
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

const LOCATION_QUERY = gql`
  query Location($id: ID!) {
    location(id: $id) {
      name
      type
      dimension
      created
      residents {
        id
        name
        status
        species
        gender
        image
      }
    }
  }
`;

export default {
  setup() {
    const route = useRoute();
    const { result, loading, error } = useQuery(LOCATION_QUERY, {
      id: route.params.id,
    });
    const location = ref(null);

    // Watch for changes in the result
    watchEffect(() => {
      if (result.value) {
        location.value = result.value.location;
      }
    });

    return {
      location,
      loading,
      error,
    };
  },
};
</script>
