<script>
import {
  VueFlux,
  FluxPreloader,
  FluxControls,
  FluxPagination,
  FluxImage,
  Img,
  Size,
  Cube,
} from "vue-flux";
import { reactive, shallowReactive } from "vue";

export default {
  components: {
    VueFlux,
    FluxPreloader,
    FluxControls,
    FluxPagination,
    FluxImage,
  },
  setup() {
    const options = reactive({
      allowFullscreen: false,
      allowToSkipTransition: true,
      autohideTime: 1500,
      autoplay: true,
      bindKeys: false,
      delay: 2000,
      enableGestures: false,
      infinite: true,
      lazyLoad: true,
      lazyLoadAfter: 3,
    });

    const rscs = shallowReactive([
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgzDyk_NKc1fi2CwUjv4d3E1YoAW1ooLFSqg&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQiNHtiOTeQ_D8Cm0Y0eE0COSun-6kRGPYUVg&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQG5FQ9no5NPjQKiS4hD9V9HfnGWn1jrRO8gw&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ9gi3T0Nq9CGBvoZnwMdwhCgvCXO6fwDOH9A&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSn6UMunCB7O4SDLZxWRr7_WdkuNt9PgA4TWA&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS5MdfIYLZz2i1BLfZkjsWTmslLtQ-3UW2yPQ&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQOIR6NNk5XuqCurjKf0uVZNeib5QSPn1jcaw&s"
      ),
      new Img(
        "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQBc_nefq6ip35Ga2gswy4qE-TKd-hp2F4Sqg&s"
      ),
    ]);

    const rsc = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRgzDyk_NKc1fi2CwUjv4d3E1YoAW1ooLFSqg&s"
    );
    const a = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQiNHtiOTeQ_D8Cm0Y0eE0COSun-6kRGPYUVg&s"
    );
    const b = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQG5FQ9no5NPjQKiS4hD9V9HfnGWn1jrRO8gw&s"
    );
    const c = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ9gi3T0Nq9CGBvoZnwMdwhCgvCXO6fwDOH9A&s"
    );
    const d = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSn6UMunCB7O4SDLZxWRr7_WdkuNt9PgA4TWA&s"
    );
    const e = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS5MdfIYLZz2i1BLfZkjsWTmslLtQ-3UW2yPQ&s"
    );
    const f = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQOIR6NNk5XuqCurjKf0uVZNeib5QSPn1jcaw&s"
    );
    const g = new Img(
      "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQBc_nefq6ip35Ga2gswy4qE-TKd-hp2F4Sqg&s"
    );
    const size = new Size({
      width: 1000, // Decreased width
      height: 650, // Decreased height
    });

    const transitions = shallowReactive([Cube]);

    return {
      options,
      rscs,
      rsc,
      size,
      transitions,
      a,
      b,
      c,
      d,
      e,
      f,
      g,
    };
  },
};
</script>

<template>
  <div class="vue-flux-container pt-20">
    <!-- <FluxImage :rsc="rsc" :size="size" />
    <FluxImage :rsc="a" :size="size" /> -->
    <!-- <FluxImage :rsc="b" :size="size" />
    <FluxImage :rsc="c" :size="size" />
    <FluxImage :rsc="d" :size="size" /> -->

    <VueFlux :options="options" :rscs="rscs" :transitions="transitions">
      <template #preloader="preloaderProps">
        <FluxPreloader v-bind="preloaderProps" />
      </template>

      <template #controls="controlsProps">
        <FluxControls v-bind="controlsProps" />
      </template>

      <template #pagination="paginationProps">
        <FluxPagination v-bind="paginationProps" />
      </template>
    </VueFlux>
  </div>
</template>

<style scoped>
.vue-flux-container {
  max-width: 1000px; /* Ensure the container size matches the image size */
  margin: auto;
}

.vue-flux-container img {
  width: 100%;
  height: auto;
}
</style>
