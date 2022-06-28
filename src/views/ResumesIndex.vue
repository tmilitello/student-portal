<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Existing Resumes",
      student: {
        personal: {
          first_name: "James",
          last_name: "Johnston",
          email: "james@test.com",
          phone_number: "123-456-7890",
          short_bio: "This is a test student.",
          linkedin: "linkedin.com/test",
          twitter_handle: "twitter.com/test",
          personal_website: "test.github.io",
          online_resume: "test.resume.com",
          github: "github.com/test",
          photo: "placeholder.jpg",
        },

        experiences: [
          { title: "Softwware Engineer", start_date: "2022-02-26", end_date: "", details: "Ran backend automation" },
          { title: "Junior Softwware Engineer", start_date: "2020-01-26", end_date: "2022-01-20", details: "Dev Ops" },
        ],

        educations: [
          {
            university: "Dartmouth College",
            degree: "Bachelor of Arts",
            start_date: "2012-08-15",
            end_date: "2016-06-14",
            details: "James got his degree in economics and Japanese history",
          },
          {
            university: "Actualize Coding Bootcamp",
            degree: "Coding Certificate",
            start_date: "2022-04-28",
            end_date: "2022-07-15",
            details: "James got his certificate in computer science",
          },
        ],

        skills: ["Ruby", "Vue.js", "Japanese", "JavaScript"],
        capstone: [
          { name: "Basketfy", description: "Thematic Investing Platform", url: "www.basketfy.io", screenshot: "hello" },
        ],
      },
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
    editModalExperiences: function (experience) {
      console.log("Show product...", experience);
      this.currentProduct = experience;
      this.editProductParams = experience;
      document.querySelector("#experiences-edit").showModal();
    },
    addModalExperiences: function (experience) {
      console.log("Show product...", experience);
      this.currentProduct = experience;
      this.editProductParams = experience;
      document.querySelector("#experiences-add").showModal();
    },
    editModalEducation: function (product) {
      console.log("Show education...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#education-edit").showModal();
    },
    addModalEducation: function (product) {
      console.log("Show education...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#education-add").showModal();
    },
    editModalSkills: function (product) {
      console.log("Show product...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#skills-edit").showModal();
    },
    editModalCapstone: function (product) {
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#capstone-edit").showModal();
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      <h2>Experience:</h2>
      <h5>
        Company Name:
        <!-- <input type="text" v-model="student.experience.start_date" /> -->
      </h5>
      <h5>Job Title: {{ "student.experience.end_date" }}</h5>
      <h5>Start Date:{{ "student.experience.job_title" }}</h5>
      <h5>End Date: {{ "student.experience.company_name" }}</h5>
      <h5>Details: {{ "student.experience.details" }}</h5>
      <button v-on:click="editModalExperiences(resume)">Edit</button>
      <button v-on:click="addModalExperiences(resume)">Add</button>
    </div>
    <div>
      <h2>Education:</h2>
      <h5>University: student.educations.start_date</h5>
      <h5>Degree: student.educations.end_date</h5>
      <h5>Start Date: student.educations.degree</h5>
      <h5>End Date: student.educations.university_name</h5>
      <h5>Details: student.educations.details</h5>
      <button v-on:click="editModalEducation(resume)">Edit</button>
      <button v-on:click="addModalEducation(resume)">Add</button>
    </div>
    <div>
      <h2>Skills:</h2>
      <h5>Skills: student.skills.skills</h5>
      <button v-on:click="editModalSkills(resume)">Edit</button>
      <!-- <button v-on:click="addModalSkills(resume)">Add</button> -->
    </div>
    <div>
      <h2>Capstone:</h2>
      <h5>Name: student.capstone.name</h5>
      <h5>Description: student.capstone.description</h5>
      <h5>URL: student.capstone.url</h5>
      <h5>Screenshot: student.capstone.screenshot</h5>
    </div>
    <button v-on:click="editModalCapstone(resume)">Edit</button>
  </div>

  <!-- Experiences -->
  <dialog id="experiences-edit">
    <form method="dialog">
      <div>
        <h1>Update Experiences</h1>
        <h5>Company Name: student.education.company_name</h5>
        <h5>Job Title: student.education.end_date</h5>
        <h5>Start Date: student.education.degree</h5>
        <h5>End Date: student.education.university_name</h5>
        <h5>Details: student.education.details</h5>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="experiences-add">
    <form method="dialog">
      <div>
        <h1>Update Experiences</h1>
        <h5>Company Name:</h5>
        <h5>Job Title:</h5>
        <h5>Start Date:</h5>
        <h5>End Date:</h5>
        <h5>Details:</h5>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="education-edit">
    <form method="dialog">
      <h1>Update Education</h1>
      <h5>University: current</h5>
      <h5>Degree: current</h5>
      <h5>Start Date: current</h5>
      <h5>End Date: current</h5>
      <h5>Details: current</h5>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
  <dialog id="education-add">
    <form method="dialog">
      <h1>Update Education</h1>
      <h5>University:</h5>
      <h5>Degree:</h5>
      <h5>Start Date:</h5>
      <h5>End Date:</h5>
      <h5>Details:</h5>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="skills-edit">
    <form method="dialog">
      <h1>Update Skills</h1>
      <h5>Skills: student.skills</h5>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <!-- Capstone -->
  <dialog id="capstone-edit">
    <form method="dialog">
      <h1>Update Capstone</h1>
      <h5>Name: v-model for student.capstone.name</h5>
      <h5>Description: v-model for student.capstone.name</h5>
      <h5>URL: v-model for student.capstone.url</h5>
      <h5>Screenshot: v-model for student.capstone.screenshot</h5>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
</template>

<style></style>
