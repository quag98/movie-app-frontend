<template>
  <div class="home">
    <h1>Movie List</h1>
    <div>
      <div v-for="movie in movies" v-bind:key="movie.id">
        <h3>{{ movie.title }}</h3>
        <button v-on:click="showMovie(movie)">Show Info</button>
    </div>
     <div>
      <button v-on:click="createMovie()">Create movie</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
    };
  },
created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/api/movies").then(response => {
        this.movies = response.data;
        console.log(this.movies);
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
      };
      axios
        .post("api/movies", params)
        .then(response => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch(error => console.log(error.response));
    },
    showMove: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
    },
    updateMove: function (movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot
      };
      axios.patch("/api/movies/" + movie.id, params).then(response => {
        console.log("OK Push", response.data);
      });
    },
        deleteMovies: function (movie) {
      axios.delete("/api/movie/" + movie.id).then(response => {
        console.log("movie has been deleted", response);
        this.$router.push("/movies");
      });
    },
  },
};
</script>