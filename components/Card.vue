<template>
  <div class="max-w-sm rounded overflow-hidden shadow-lg bg-white my-4 flex flex-col mx-2">
    <img class="w-full" :src="this.image" alt="Sunset in the mountains" />
    <div class="px-6 py-4">
      <div class="font-bold text-xl mb-2">{{this.title}}</div>
      <p class="text-gray-700 text-base">{{this.description}}</p>
    </div>
  </div>
</template>

<script>
module.exports = {
  name: "card",
  props: ["image", "title", "description"]
};
</script>