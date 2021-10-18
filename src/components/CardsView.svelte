<script>
  import { onMount } from "svelte";
  import Card from "./Card.svelte";

  let projects = [];

  onMount(() => {
    let localProjects = localStorage.getItem("projects");
    if (localProjects) {
      projects = JSON.parse(localProjects);
    }
    fetch("https://api.kaustav.ml/projects")
      .then((data) => data.json())
      .then((data) => {
        projects = data;
        localStorage.setItem("projects", JSON.stringify(data));
      });
  });

  function getScreenshotLink(website) {
    const urlWIthoutProtocol = website.split("://")[1];
    return `https://cdn.statically.io/screenshot/${urlWIthoutProtocol}`;
  }
</script>

<div class="grid grid-cols-1 md:grid-cols-3">
  {#each projects as project}
    <Card
      image={getScreenshotLink(project.url)}
      url={project.url}
      title={project.name}
      description={project.description}
    />
  {/each}
</div>
