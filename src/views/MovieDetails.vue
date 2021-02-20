<template>
  <div class="movie-details">
    <h2>Movie Title {{ $route.params.id }}</h2>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/env.js";

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => {
          response.json();
        })
        .then((data) => {
          console.log(data);
        });
    });
    return {
      movie,
    };
  },
};
</script>

<style>
</style>