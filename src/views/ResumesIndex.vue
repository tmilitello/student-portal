<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Resume",
      newStudentParams: {},
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
            company_name: "Apple",
            job_title: "Softwware Engineer",
            start_date: "2022-02-26",
            end_date: "current",
            details: "Ran backend automation",
          },
          {
            company_name: "Google",
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
      <h2>{{ experience.company_name }}</h2>
      <h4>Job Title: {{ experience.job_title }}</h4>
      <h5>Start Date: {{ experience.start_date }}</h5>
      <h5>End Date: {{ experience.end_date }}</h5>
      <h5>Details: {{ experience.details }}</h5>
      <button v-on:click="editModalExperiences(resume)">Edit</button>
      <button v-on:click="addModalExperiences(resume)">Add</button>
    </div>
    <div>
      <h2>Education:</h2>
      <div v-for="education in student.educations" v-bind:key="education.id">
        <h2>{{ education.university_name }}</h2>
        <h4>Degree: {{ education.degree }}</h4>
        <h5>Start Date: {{ education.start_date }}</h5>
        <h5>End Date: {{ education.end_date }}</h5>
        <h5>Details: {{ education.details }}</h5>
        <button v-on:click="editModalEducation(resume)">Edit</button>
        <button v-on:click="addModalEducation(resume)">Add</button>
      </div>
    </div>
    <div>
      <h2>Skills:</h2>
      <div v-for="skill in student.skills" v-bind:key="skill.id">
        <h5>{{ skill }}</h5>
      </div>
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
      <h1>Update Experiences</h1>
      <div v-for="experience in student.experiences" v-bind:key="experience.id">
        <div>
          Company Name:
          <input type="text" v-model="experience.company_name" />
        </div>
        <div>
          Job Title:
          <input type="text" v-model="experience.job_title" />
        </div>
        <div>
          Start Date:
          <input type="text" v-model="experience.start_date" />
        </div>
        <div>
          End Date:
          <input type="text" v-model="experience.end_date" />
        </div>
        <div>
          Details:
          <input type="text" v-model="experience.details" />
        </div>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="experiences-add">
    <form method="dialog">
      <div>
        <h1>Add Experiences</h1>
        <div>
          Company Name:
          <input type="text" v-model="newStudentParams.company_name" />
        </div>
        <div>
          Job Title:
          <input type="text" v-model="newStudentParams.job_title" />
        </div>
        <div>
          Start Date:
          <input type="text" v-model="newStudentParams.start_date" />
        </div>
        <div>
          End Date:
          <input type="text" v-model="newStudentParams.end_date" />
        </div>
        <div>
          Details:
          <input type="text" v-model="newStudentParams.details" />
        </div>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="education-edit">
    <form method="dialog">
      <h1>Update Education</h1>
      <div v-for="education in student.educations" v-bind:key="education.id">
        <div>
          University:
          <input type="text" v-model="education.university_name" />
        </div>
        <div>
          Degree:
          <input type="text" v-model="education.degree" />
        </div>
        <div>
          Start Date:
          <input type="text" v-model="education.start_date" />
        </div>
        <div>
          End Date:
          <input type="text" v-model="education.end_date" />
        </div>
        <div>
          Details:
          <input type="text" v-model="education.details" />
        </div>
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
  <dialog id="education-add">
    <form method="dialog">
      <h1>Add Education</h1>
      <div>
        University:
        <input type="text" v-model="newStudentParams.university_name" />
      </div>
      <div>
        Degree:
        <input type="text" v-model="newStudentParams.degree" />
      </div>
      <div>
        Start Date:
        <input type="text" v-model="newStudentParams.start_date" />
      </div>
      <div>
        End Date:
        <input type="text" v-model="newStudentParams.end_date" />
      </div>
      <div>
        Details:
        <input type="text" v-model="newStudentParams.details" />
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <dialog id="skills-edit">
    <form method="dialog">
      <h1>Update Skills</h1>
      <!-- <div v-for="skill in student.skills" v-bind:key="skill.id"> -->
      <div>
        Skills:
        <input type="text" v-model="student.skills" />
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>

  <!-- Capstone -->
  <dialog id="capstone-edit">
    <form method="dialog">
      <div>
        Name:
        <input type="text" v-model="student.capstone.name" />
      </div>
      <div>
        Description:
        <input type="text" v-model="student.capstone.description" />
      </div>
      <div>
        URL:
        <input type="text" v-model="student.capstone.url" />
      </div>
      <div>
        Screenshot:
        <input type="text" v-model="student.capstone.screenshot" />
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
</template>

<style></style>
