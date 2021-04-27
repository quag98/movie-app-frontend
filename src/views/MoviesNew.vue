<template>
  <div class="container movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label>
        <input type="text" class="form-control" v-model="title" />
      </div>
      <div class="form-group">
        <label>Year:</label>
        <input type="text" class="form-control" v-model="year" />
      </div>
      <div class="form-group">
        <label>Plot:</label>
        <input type="text" class="form-control" v-model="plot" />
      </div>
      <input type="submit" class="btn btn-primary" value="Submit" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      title: "",
      year: "",
      plot: "",
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      console.log("Creating a Movie!");
      var params = {
        title: this.title,
        year: this.year,
        plot: this.plot,
      };
      axios
        .post("/api/movies", params)
        .then(() => {
          this.$router.push("/movies");
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>
