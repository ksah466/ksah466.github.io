<script>
  import { onMount } from "svelte";
  import Card from "./Card.svelte";

  let projects = [];

  onMount(() => {
    let localProjects = localStorage.getItem("projects");
    if (localProjects) {
      projects = JSON.parse(localProjects);
    }
    fetch("https://api.kaustav.ml/projects.json")
      .then((data) => data.json())
      .then(({ data }) => {
        projects = data;
        localStorage.setItem("projects", JSON.stringify(data));
      });
  });
</script>

<div class="grid grid-cols-1 md:grid-cols-3">
  {#each projects as project}
    <Card
      image={`https://image.thum.io/get/${project.homepage}`}
      url={project.homepage}
      title={project.name}
      description={project.description} />
  {/each}
</div>
