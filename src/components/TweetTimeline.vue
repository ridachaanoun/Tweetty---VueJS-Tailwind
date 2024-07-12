<template>
  <div class="flex justify-center  min-h-screen bg-white">

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
