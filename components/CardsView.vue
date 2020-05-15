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
    fetch("https://api.github.com/users/ksah466/repos")
      .then(response => response.json())
      .then(response =>
        response
          .filter(
            element =>
              element["has_pages"] &&
              element["homepage"] != null &&
              element["name"] != "ksah466.github.io"
          )
          .map(({ name, description, homepage, updated_at }) => {
            return {
              name,
              description,
              homepage,
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