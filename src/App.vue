<template>

 

    <div  >
      <TweetTimeline />
    </div>
   
</template>

<script>

import TweetTimeline from './components/TweetTimeline.vue';



export default {
  name: 'App',
  components: {
    TweetTimeline
    
  }
};
</script>

<style>
body {
  font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background-color: #f5f8fa;
}
</style>
