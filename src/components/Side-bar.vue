<template>
  <aside class="w-1/4 p-4 pl-10">
    <div class="sticky top-0">
      <i class="fab fa-twitter text-4xl text-sky-400"></i>
      <nav class="space-y-2 mt-4">
        <a href="#" class="flex items-center space-x-3 p-2 text-lg font-bold text-sky-400 hover:bg-blue-100 rounded-full">
          <i class="fas fa-home"></i>
          <span>Home</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-hashtag"></i>
          <span>Explore</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-bell"></i>
          <span>Notifications</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-envelope"></i>
          <span>Messages</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-bookmark"></i>
          <span>Bookmarks</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-list"></i>
          <span>Lists</span>
        </a>
        <a href="" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRXJA32WU4rBpx7maglqeEtt3ot1tPIRWptxA&s" alt="" class="h-8 w-8 rounded-full">
          <span>Profile</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <i class="fas fa-ellipsis-h"></i>
          <span>More</span>
        </a>
      </nav>
      <button class="mt-6 bg-sky-400 text-white py-2 px-4 rounded-full w-full max-w-80">Tweet</button>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'Sid-ebar'
};
</script>
<!-- -->