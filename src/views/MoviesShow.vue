<template>
  <div class="movies-show">
    <div>
      <h2>{{  movie.title  }}</h2>
      <li>
        <ol> <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit movie</router-link> </ol>
        <ol> <button v-on:click="deleteMovies(movie)">Delete movie</button> </ol>
      </li>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h3>{{ movie.year }}</h3>
        <p>{{ movie.plot }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    this.showMovies();
  },
  methods: {
    showMovies: function () {
      axios.get("/api/movies/" + this.$route.params.id).then((response) => {
        console.log("movies show", response);
        this.movie = response.data;
      });
    },
    deleteMovies: function (movie) {
      axios.delete("/api/movies/" + movie.id).then(response => {
        console.log("move has been deleted", response);
        this.$router.push("/movies");
      });
    },
  },
};
</script>