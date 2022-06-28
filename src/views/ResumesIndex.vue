<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Existing Resumes",
      student: {},
      resumeParams: {},
    };
  },
  created: function () {},
  methods: {
    showStudent: function () {
      axios.get("/students/1.json").then((response) => {
        console.log("Showing student resume");
        this.student = response.data;
      });
    },
    updateResume: function () {},
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- Experience, Education, Skills, Capstone -->
  </div>
</template>

<style></style>
