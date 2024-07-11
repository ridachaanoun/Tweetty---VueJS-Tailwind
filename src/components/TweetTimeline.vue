<template>
  <div class="flex justify-center bg-gray-100 min-h-screen">

      <Sidebar />
      <MainContent />
      <TrendsSuggestions />

  </div>
</template>

<script>
import Sidebar from './Side-bar.vue';
import MainContent from './MainContent.vue';
import TrendsSuggestions from './TrendsSuggestions.vue';

export default {
  name: 'TweetTimeline',
  components: {
    Sidebar,
    MainContent,
    TrendsSuggestions,
  }
};
</script>
