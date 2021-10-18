<script>
  export let title;
  export let description;
  export let image;
  export let url;
</script>

<div class="m-2 max-w-sm rounded overflow-hidden shadow-lg flex flex-col">
  <img class="w-full" src={image} alt={title} />
  <div class="px-4 py-2">
    <div class="font-bold text-xl mb-2">{title}</div>
    <p class="text-gray-700 text-base">{description}</p>
  </div>
  <div class="p-4 mt-auto">
    <a
      href={url}
      class="inline-block bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    >
      Visit
    </a>
  </div>
</div>
