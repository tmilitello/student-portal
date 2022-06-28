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
    updateStudent: function () {},
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      <h2>Experience:</h2>
      <p>
        Start date:
        <!-- <input type="text" v-model="student.experience.start_date" /> -->
      </p>
      <p>End date: {{ "student.experience.end_date" }}</p>
      <p>Job Title:{{ "student.experience.job_title" }}</p>
      <p>Company Name: {{ "student.experience.company_name" }}</p>
      <p>Details: {{ "student.experience.details" }}</p>
    </div>
    <div>
      <h2>Education:</h2>
      <p>Start date: student.education.start_date</p>
      <p>End date: student.education.end_date</p>
      <p>Graduation: student.education.degree</p>
      <p>University name: student.education.university_name</p>
      <p>Details: student.education.details</p>
    </div>
    <div>
      <h2>Skills:</h2>
      <p>student.skills.skill_name</p>
    </div>
    <div>
      <h2>Capstone:</h2>
      <p>Name: student.capstone.name</p>
      <p>Description: student.capstone.description</p>
      <p>URL: student.capstone.url</p>
      <p>Screenshot: student.capstone.screenshot</p>
    </div>
    <button v-on:click="updateStudent()">Save</button>
  </div>
</template>

<style></style>
