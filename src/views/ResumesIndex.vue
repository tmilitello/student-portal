<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Existing Resumes",
      student: {
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
        experiences: [
          {
            company_name: "Company",
            job_title: "Softwware Engineer",
            start_date: "2022-02-26",
            end_date: "current",
            details: "Ran backend automation",
          },
          {
            company_name: "Other Company",
            job_title: "Junior Softwware Engineer",
            start_date: "2020-01-26",
            end_date: "2022-01-20",
            details: "Dev Ops",
          },
        ],
        educations: [
          {
            university_name: "Dartmouth College",
            degree: "Bachelor of Arts",
            start_date: "2012-08-15",
            end_date: "2016-06-14",
            details: "James got his degree in economics and Japanese history",
          },
          {
            university_name: "Actualize Coding Bootcamp",
            degree: "Coding Certificate",
            start_date: "2022-04-28",
            end_date: "2022-07-15",
            details: "James got his certificate in computer science",
          },
        ],
        skills: ["Ruby", "Vue.js", "Japanese", "JavaScript"],
        capstone: {
          name: "Basketfy",
          description: "Thematic Investing Platform",
          url: "www.basketfy.io",
          screenshot: "hello",
        },
      },
      resumeParams: {},
    };
  },
  created: function () {
    console.log(this.student);
    console.log(this.student.experiences);
    console.log(this.student.educations);
    console.log(this.student.capstone.name);
  },
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
    <h2>Experience:</h2>
    <div v-for="experience in student.experiences" v-bind:key="experience.id">
      <h5>Company Name: {{ experience.company_name }}</h5>
      <h5>Job Title: {{ experience.job_title }}</h5>
      <h5>Start Date:{{ experience.start_date }}</h5>
      <h5>End Date: {{ experience.end_date }}</h5>
      <h5>Details: {{ experience.details }}</h5>
      <button v-on:click="editModalExperiences(resume)">Edit</button>
      <button v-on:click="addModalExperiences(resume)">Add</button>
    </div>
    <div>
      <h2>Education:</h2>
      <div v-for="education in student.educations" v-bind:key="education.id">
        <h5>University Name: {{ education.university_name }}</h5>
        <h5>Degree: {{ education.degree }}</h5>
        <h5>Start Date: {{ education.start_date }}</h5>
        <h5>End Date: {{ education.end_date }}</h5>
        <h5>Details: {{ education.details }}</h5>
        <button v-on:click="editModalEducation(resume)">Edit</button>
        <button v-on:click="addModalEducation(resume)">Add</button>
      </div>
    </div>
    <div>
      <h2>Skills:</h2>
      <h5>{{ student.skills }}</h5>
      <button v-on:click="editModalSkills(resume)">Edit</button>
      <!-- <button v-on:click="addModalSkills(resume)">Add</button> -->
    </div>
    <div>
      <h2>Capstone:</h2>
      <h5>Name: {{ student.capstone.name }}</h5>
      <h5>Description: {{ student.capstone.description }}</h5>
      <h5>URL: {{ student.capstone.url }}</h5>
      <h5>Screenshot: {{ student.capstone.screenshot }}</h5>
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
