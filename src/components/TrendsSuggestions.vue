<template>
  <aside class="w-1/4 p-4 sticky top-0 right-0 mr-9">
    <div class="px-3 py-2  rounded-3xl flex items-center relative mb-4 bg-slate-100">
      <i class="fa-solid fa-magnifying-glass text-slate-500"></i>
      <input class="bg-transparent w-full outline-none pl-3" type="text" placeholder="Search Twitter">
    </div>
    <div class="bg-slate-100 p-4 rounded-lg shadow w-auto ">
      <h2 class="text-lg font-bold mb-4 flex justify-between items-center">Trends for you <i class="fa-solid fa-gear text-sky-400"></i></h2>
      <ul class="space-y-2">
        <li class="text-gray-700">
          <strong>#NationalAuthorsDay</strong>
          <p class="text-sm text-gray-500">Trending worldwide with: #AuthorsDay</p>
          <p class="text-sm text-gray-500">4 Tina Koyama is Tweeting about this</p>
        </li>
        <li class="text-gray-700">
          <strong>#SkincareSunday</strong>
          <p class="text-sm text-gray-500">125K Tweets, 5,094 people are Tweeting about this</p>
        </li>
        <li class="text-gray-700">
          <strong>#InternationalCatDay</strong>
          <p class="text-sm text-gray-500">Animals. These cats are ready for #InternationalCatDay</p>
          <p class="text-sm text-gray-500">2,757 people are Tweeting about this</p>
        </li>
        <li class="text-gray-700">
          <strong>Spice Girls Tour</strong>
          <p class="text-sm text-gray-500">125K Tweets. Tina Koyama is Tweeting about this</p>
        </li>
        <li class="text-gray-700">
          <strong>#Huskers</strong>
          <p class="text-sm text-gray-500">Trending worldwide with: #Nebraska. 5,094 people are Tweeting about this</p>
        </li>
      </ul>
      <h2 class="text-lg font-bold mb-4">Who to follow</h2>
      <ul class="space-y-2">
        <li class="flex items-center space-x-2">
          <img src="https://randomuser.me/api/portraits/men/1.jpg" alt="John Doe" class="h-8 w-8 rounded-full">
          <span class="text-blue-500">@JohnDoe</span>
        </li>
        <li class="flex items-center space-x-2">
          <img src="https://randomuser.me/api/portraits/women/1.jpg" alt="Jane Smith" class="h-8 w-8 rounded-full">
          <span class="text-blue-500">@JaneSmith</span>
        </li>
        <li class="flex items-center space-x-2">
          <img src="https://randomuser.me/api/portraits/men/2.jpg" alt="Random User" class="h-8 w-8 rounded-full">
          <span class="text-blue-500">@RandomUser</span>
        </li>
      </ul>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'TrendsSuggestions'
};
</script>

<style scoped>
/* Add any additional styles here */
</style>
