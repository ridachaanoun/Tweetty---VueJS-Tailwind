<template>
  <aside class="w-1/4 p-4">
    <div class="bg-white p-4 rounded-lg shadow">
      <h2 class="text-lg font-bold mb-4">Trends for you</h2>
      <ul class="space-y-2">
        <li class="text-gray-700">#NationalAuthorsDay</li>
        <li class="text-gray-700">#SkincareSunday</li>
        <li class="text-gray-700">#InternationalCatDay</li>
      </ul>
    </div>
    <div class="bg-white p-4 rounded-lg shadow mt-4">
      <h2 class="text-lg font-bold mb-4">Who to follow</h2>
      <ul class="space-y-2">
        <li class="text-blue-500">@JohnDoe</li>
        <li class="text-blue-500">@JaneSmith</li>
        <li class="text-blue-500">@RandomUser</li>
      </ul>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'TrendsSuggestions'
};
</script>
