<template>
  <div class="home">
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h3>{{ movie.title }}</h3>
        <p>{{ movie.user }}</p>
        <router-link v-bind:to="`/movies/${movie.id}`">More Info</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexPosts: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log("all movies:", this.movies);
      });
    },
  },
};
</script>