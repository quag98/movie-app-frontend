<template>
  <div class="container movies-edit">
    <form v-on:submit.prevent="updateMovie()">
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
  data: function() {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function() {
    axios.get("/api/posts/" + this.$route.params.id).then(response => {
      console.log(response);
      this.post = response.daa;
    });
  },
  methods: {
    updatePost: function(post) {
      var params = {
        title: post.title,
        body: post.body,
        image: post.image,
      };
      axios
        .patch("/api/photos/" + post.id, params)
        .then(response => { 
          console.log("post updated", response);
          this.$router.push("/posts");
        });
    },
  },
};
</script>