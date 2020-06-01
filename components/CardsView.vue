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
    Promise.all([this.getGithub(), this.getGlitch(), this.getCustom()]).then(
      values => {
        let allProjects = values
          .flat()
          .sort((a, b) => new Date(b.updated_at) - new Date(a.updated_at));
        console.log(allProjects);
        this.projects = allProjects;
      }
    );
  },
  data() {
    return {
      projects: []
    };
  },
  methods: {
    getGithub() {
      return fetch("https://api.github.com/users/ksah466/repos")
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
        );
    },
    getGlitch() {
      return fetch(
        "https://api.glitch.com/v1/collections/by/id/projects?id=55957&limit=100"
      )
        .then(response => response.json())
        .then(({ items }) =>
          items.map(({ domain, description, updatedAt }) => {
            return {
              name: domain,
              description,
              homepage: `https://${domain}.glitch.me`,
              updated_at: updatedAt
            };
          })
        );
    },
    getCustom() {
      return fetch(
        "https://gist.githubusercontent.com/ksah466/b21a03b47585eb87a99181a29e48cd19/raw/projects.json"
      )
        .then(data => data.json())
        .then(({ projects }) => projects);
    }
  },
  components: {
    card: window.httpVueLoader("./components/Card.vue")
  }
};
</script>