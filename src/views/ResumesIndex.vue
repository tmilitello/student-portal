<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Existing Resumes",
      resumes: [],
    };
  },
  created: function () {},
  methods: {
    IndexResumes: function () {
      axios.get("/resumes").then((response) => {
        console.log("indexing resumes?");
        this.resumes = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
  </div>
</template>

<style></style>
