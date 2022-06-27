<script>
export default {
  data: function () {
    return {
      message: "",
      resume: {},
    };
  },
  created: function () {
    axios.get("/resumes/" + this.$route.params.id).then((response) => {
      console.log("Resume Show");
      console.log(response.data);
      this.resume = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="resume-show">
    <h1>{{ message }}</h1>
  </div>
</template>

<style></style>
