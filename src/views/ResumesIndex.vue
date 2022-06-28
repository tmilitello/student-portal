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
    <div>
      <h2>Experience:</h2>
      <p>{{ "student.experience.start_date" }}</p>
      <p>{{ "student.experience.end_date" }}</p>
      <p>{{ "student.experience.job_title" }}</p>
      <p>{{ "student.experience.company_name" }}</p>
      <p>{{ "student.experience.details" }}</p>
    </div>
    <div>
      <h2>Education:</h2>
      <p>student.education.start_date</p>
      <p>student.education.end_date</p>
      <p>student.education.degree</p>
      <p>student.education.university_name</p>
      <p>student.education.details</p>
    </div>
    <div>
      <h2>Skills:</h2>
      <p>student.skills.skill_name</p>
    </div>
    <div>
      <h2>Capstone:</h2>
      <p>student.capstone.name</p>
      <p>student.capstone.description</p>
      <p>student.capstone.url</p>
      <p>student.capstone.screenshot</p>
    </div>
    <!-- Experience, Education, Skills, Capstone -->
  </div>
</template>

<style></style>
