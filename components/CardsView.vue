<template>
  <div class="grid grid-cols-1 md:grid-cols-2">
    <div v-for="project in projects" :key="project.name">
      <card
        :image="`https://image.thum.io/get/https://kaustav.ml/${project.name}`"
        :title="project.name"
        :description="project.description"
      />
    </div>
  </div>
</template>

<script>
module.exports = {
  mounted() {
    fetch("https://api.github.com/users/ksah466/repos")
      .then(response => response.json())
      .then(response =>
        response
          .filter(
            element =>
              element["has_pages"] && element["name"] != "ksah466.github.io"
          )
          .map(({ name, description, updated_at }) => {
            return {
              name,
              description,
              updated_at
            };
          })
      )
      .then(data => (this.projects = data));
  },
  data() {
    return {
      projects: null
    };
  },
  components: {
    card: window.httpVueLoader("./components/Card.vue")
  }
};
</script>

<style>
</style>