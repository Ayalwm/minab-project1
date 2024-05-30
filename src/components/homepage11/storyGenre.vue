<template>
  <div class="z-50 p-4 flex justify-end">
    <!-- Second column with show information -->
    <div class="flex-grow max-w-xl">
      <div
        class="bg-white border border-gray-200 rounded-lg shadow-md p-14 animated">
        <div class="mb-8">
          <h3
            class="text-lg font-semibold text-gray-700 border-l-4 border-blue-500 pl-4 mb-4">
            <i class="fas fa-book-open text-xl mr-2"></i> Storyline:
          </h3>
          <p class="text-gray-600 ml-6">{{ show.storyline }}</p>
        </div>
        <div class="mb-8">
          <h3
            class="text-lg font-semibold text-gray-700 border-l-4 border-blue-500 pl-4 mb-4">
            <i class="fas fa-film text-xl mr-2"></i> Genre:
          </h3>
          <p class="text-gray-600 ml-6">{{ show.genre }}</p>
        </div>
        <div class="mb-8">
          <h3
            class="text-lg font-semibold text-gray-700 border-l-4 border-blue-500 pl-4 mb-4">
            <i class="fas fa-user-edit text-xl mr-2"></i> Creators:
          </h3>
          <p class="text-gray-600 ml-6">{{ show.creators }}</p>
        </div>
        <div class="mb-8">
          <h3
            class="text-lg font-semibold text-gray-700 border-l-4 border-blue-500 pl-4 mb-4">
            <i class="fas fa-star text-xl mr-2"></i> Stars:
          </h3>
          <p class="text-gray-600 ml-6">{{ show.stars }}</p>
        </div>
        <div>
          <h3
            class="text-lg font-semibold text-gray-700 border-l-4 border-blue-500 pl-4 mb-4">
            <i class="fas fa-star-half-alt pulsating-icon text-xl mr-2"></i>
            Rating:
          </h3>
          <p class="text-gray-600 ml-6">
            <span v-for="n in 5" :key="n" class="text-yellow-500">
              <i
                class="fas fa-star"
                v-if="n <= Math.floor(show.rating / 2)"></i>
              <i
                class="fas fa-star-half-alt"
                v-else-if="n === Math.ceil(show.rating / 2)"></i>
              <i class="far fa-star" v-else></i>
            </span>
            ({{ show.rating }} / 10)
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const show = {
  storyline:
    "An animated series that follows the misadventures of an eccentric scientist and his good-hearted but easily influenced grandson.",
  genre: "Animation, Adventure, Comedy",
  creators: "Dan Harmon, Justin Roiland",
  stars: "Justin Roiland, Chris Parnell, Spencer Grammer",
  rating: 8, // Changed to a numerical value for better handling
};
</script>

<style scoped>
/* Animation */
@keyframes fadeInRight {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.animated {
  animation: fadeInRight 0.5s ease-in-out;
}

@keyframes pulse {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

.pulsating-icon {
  display: inline-block;
  animation: pulse 1.5s infinite;
}
</style>
