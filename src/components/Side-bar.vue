<template>
  <aside class="w-1/4 p-4 ">
    <div class="sticky top-0">
      <i class="fa-brands fa-twitter text-4xl" style="color: #74C0FC;"></i>
      <nav class="space-y-2">
        
        <a href="../assets/icons/home.svg" class="flex items-center space-x-3 p-2 text-lg font-bold text-blue-500 hover:bg-blue-100 rounded-full">
          <span>Home</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Explore</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Notifications</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Messages</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Bookmarks</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Lists</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>Profile</span>
        </a>
        <a href="#" class="flex items-center space-x-3 p-2 text-lg text-gray-700 hover:bg-blue-100 rounded-full">
          <span>More</span>
        </a>
      </nav>
      <button class="mt-6 bg-blue-500 text-white py-2 px-4 rounded-full w-full">Tweet</button>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'Side-bar'
};
</script>
