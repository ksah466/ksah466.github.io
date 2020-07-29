<template>
  <div class="grid grid-cols-1 md:grid-cols-3">
    <card
      v-for="project in projects"
      :key="project.name"
      :image="`https://image.thum.io/get/${project.homepage}`"
      :url="project.homepage"
      :title="project.name"
      :description="project.description"
    />
  </div>
</template>

<script>
module.exports = {
  mounted() {
    let localProjects = localStorage.getItem("projects");
    if (localProjects) {
      this.projects = JSON.parse(localProjects);
    }
    fetch("https://api.kaustav.ml/projects.json")
      .then((data) => data.json())
      .then(({ data }) => {
        this.projects = data;
        localStorage.setItem("projects", JSON.stringify(data));
      });
  },
  data() {
    return {
      projects: [],
    };
  },
  components: {
    card: window.httpVueLoader("./components/Card.vue"),
  },
};
</script>
