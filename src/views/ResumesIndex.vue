<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Resume",
      newStudentParams: {},
      newSkillParams: {},
      student: {},
      resumeParams: {},
    };
  },
  created: function () {
    this.showStudent();
    console.log(this.student);
    console.log(this.student.experiences);
    console.log(this.student.educations);
    console.log(this.student.capstones);
  },
  methods: {
    showStudent: function () {
      axios.get("/students/" + localStorage.user_id + ".json").then((response) => {
        console.log("Showing student resume", response.data);
        this.student = response.data;
      });
    },
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
    addModalSkills: function (product) {
      console.log("Show product...", product);
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#skills-add").showModal();
    },
    editModalCapstone: function (product) {
      this.currentProduct = product;
      this.editProductParams = product;
      document.querySelector("#capstone-edit").showModal();
    },
    createSkill: function () {
      axios.post("/student_skills.json", this.newSkillParams).then((response) => {
        console.log(response.data);
        this.student.skills.push(response.data);
        this.newSkillParams = {};
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>Experience:</h2>
    <button v-on:click="editModalExperiences(resume)">Edit</button>
    <button v-on:click="addModalExperiences(resume)">Add</button>
    <div v-for="experience in student.experiences" v-bind:key="experience.id">
      <h2>{{ experience.company_name }}</h2>
      <h4>Job Title: {{ experience.job_title }}</h4>
      <h5>Start Date: {{ experience.start_date }}</h5>
      <h5>End Date: {{ experience.end_date }}</h5>
      <h5>Details: {{ experience.details }}</h5>
    </div>
    <div>
      <h2>Education:</h2>
      <button v-on:click="editModalEducation(resume)">Edit</button>
      <button v-on:click="addModalEducation(resume)">Add</button>
      <div v-for="education in student.educations" v-bind:key="education.id">
        <h2>{{ education.university_name }}</h2>
        <h4>Degree: {{ education.degree }}</h4>
        <h5>Start Date: {{ education.start_date }}</h5>
        <h5>End Date: {{ education.end_date }}</h5>
        <h5>Details: {{ education.details }}</h5>
      </div>
    </div>
    <div>
      <h2>Skills:</h2>
      <!-- <button v-on:click="editModalSkills(resume)">Edit</button>
      <button v-on:click="addModalSkills(resume)">Add</button> -->
      <div v-for="skill in student.student_skills" v-bind:key="skill.id">
        <h5>{{ skill.skill_name }}</h5>
      </div>
    </div>
    <div>
      <h2>Capstone:</h2>
      <div v-for="capstone in student.capstones" v-bind:key="capstone.id">
        <button v-on:click="editModalCapstone(resume)">Edit</button>
        <h5>Name: {{ capstone.name }}</h5>
        <h5>Description: {{ capstone.description }}</h5>
        <h5>URL: {{ capstone.url }}</h5>
        <h5>Screenshot: {{ capstone.screenshot }}</h5>
      </div>
    </div>
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

  <dialog id="skills-add">
    <form method="dialog">
      <h1>Update Skills</h1>
      <!-- <div v-for="skill in student.skills" v-bind:key="skill.id"> -->
      <div>
        Skill Name:
        <input type="text" v-model="newSkillParams.skill_name" />
      </div>
      <p><button v-on:click="createSkill()">Update</button></p>
    </form>
  </dialog>

  <dialog id="capstone-edit">
    <form method="dialog">
      <div>
        Name:
        <input type="text" v-model="student.capstones.name" />
      </div>
      <div>
        Description:
        <input type="text" v-model="student.capstones.description" />
      </div>
      <div>
        URL:
        <input type="text" v-model="student.capstones.url" />
      </div>
      <div>
        Screenshot:
        <input type="text" v-model="student.capstones.screenshot" />
      </div>
      <p><button v-on:click="updateStudent(student)">Update</button></p>
    </form>
  </dialog>
</template>

<style></style>
