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
    showModalExperiences: function (experience) {
      console.log("Show product...", experience);
      this.currentProduct = experience;
      this.editProductParams = experience;
      document.querySelector("#experiences-details").showModal();
    },
    showModalEducation: function (product) {
      console.log("Show education...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#education-details").showModal();
    },
    showModalSkills: function (product) {
      console.log("Show product...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#product-details").showModal();
    },
    showModalCapstone: function (product) {
      console.log("Show product...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#product-details").showModal();
    },
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
      <button v-on:click="showModalExperiences(resume)">Update</button>
    </div>
    <div>
      <h2>Education:</h2>
      <p>Start date: student.education.start_date</p>
      <p>End date: student.education.end_date</p>
      <p>Graduation: student.education.degree</p>
      <p>University name: student.education.university_name</p>
      <p>Details: student.education.details</p>
      <button v-on:click="showModalEducation(resume)">Update</button>
    </div>
    <div>
      <h2>Skills:</h2>
      <p>student.skills.skill_name</p>
      <button v-on:click="showModalSkills(resume)">Update</button>
    </div>
    <div>
      <h2>Capstone:</h2>
      <p>Name: student.capstone.name</p>
      <p>Description: student.capstone.description</p>
      <p>URL: student.capstone.url</p>
      <p>Screenshot: student.capstone.screenshot</p>
    </div>
    <button v-on:click="showModalCapstone(resume)">Update</button>
  </div>

  <!-- Experiences -->
  <dialog id="experiences-details">
    <form method="dialog">
      <div>
        <h1>Update Experiences</h1>
        <p>Start date: student.education.start_date</p>
        <p>End date: student.education.end_date</p>
        <p>Graduation: student.education.degree</p>
        <p>University name: student.education.university_name</p>
        <p>Details: student.education.details</p>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="education-details">
    <form method="dialog">
      <h2>Education</h2>
      <h4>University Name:</h4>
      <h4>Degree:</h4>
      <h4>Start Date:</h4>
      <h4>End Date:</h4>
      <h4>Details:</h4>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="product-details">
    <form method="dialog">
      <p>Hello</p>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <!-- Capstone -->
  <dialog id="product-details">
    <form method="dialog">
      <p>Hello</p>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
</template>

<style></style>
