<template>
  <main class="w-1/2  px-0 border">
    <Home />
    <div class="bg-b p-4 mb-4 border-b">
      <form @submit.prevent="addTweet" class="flex space-x-4 items-center">
        <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRXJA32WU4rBpx7maglqeEtt3ot1tPIRWptxA&s" alt="User Avatar" class="h-10 w-10 rounded-full">
        <input v-model="newTweet" type="text" placeholder="What's happening?" class="flex-1 p-2 border rounded-lg" required />
        <!-- <button type="submit" class="bg-blue-500 text-white py-2 px-4 rounded-full">Tweet</button> -->
        <i class="fa-solid fa-image" style="color: #74C0FC;"></i>
        <i class="fa-solid fa-gift" style="color: #74C0FC;"></i>
        <i class="fa-solid fa-chart-simple fa-rotate-90" style="color: #74C0FC;"></i>
      </form>
    </div >
    <ul class="space-y-4">
      <li v-for="tweet in tweets" :key="tweet.id" class="bg-white p-4  border-b ">
        <div class="flex space-x-4">
          <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRXJA32WU4rBpx7maglqeEtt3ot1tPIRWptxA&s" alt="User Avatar" class="h-10 w-10 rounded-full">
          <div>
            <div class="text-gray-900">{{ tweet.user }} - {{ formatDate(tweet.created_at) }}</div>
            <div class="text-gray-900 break-all" >{{ tweet.content }}</div>
            <div class="flex space-x-2 text-gray-500 text-sm mt-2 w-60 justify-around">
              <button @click="toggleLike(tweet.id)" class="flex items-center space-x-1">
                <i :class="tweet.liked ? 'fa-solid fa-heart text-red-600' : 'fa-solid fa-heart text-gray-500'"></i>
                <span>{{ tweet.likes }}</span>
              </button>
              <button @click="toggleRetweet(tweet.id)" :class="{'text-green-600': tweet.retweeted}" class="flex items-center space-x-1">
                <i class="fa-solid fa-retweet"></i>
                <span>{{ tweet.retweets }}</span>
              </button>
              <button @click="toggleReplyBox(tweet.id)" class="flex items-center space-x-1">
                <i class="fa-solid fa-reply"></i>
                <span>Reply</span>
              </button>
            </div>
            <div v-if="tweet.showReplyBox" class="mt-2">
              <form @submit.prevent="addReply(tweet.id)" class="flex space-x-2">
                <input v-model="newReply" type="text" placeholder="Write a reply..." class="flex-1 p-2 border rounded-lg" required />
                <button type="submit" class="bg-blue-500 text-white py-1 px-4 rounded-full">Reply</button>
              </form>
              <ul v-if="tweet.replies && tweet.replies.length" class="mt-2 space-y-2">
                <li v-for="reply in tweet.replies" :key="reply.id" class="text-gray-700 text-sm">
                  <img src="user-avatar.png" alt="User Avatar" class="inline-block h-6 w-6 rounded-full mr-2">
                  {{ reply.content }}
                </li>
              </ul>
            </div>
          </div>
        </div>
      </li>
    </ul>
  </main>
</template>

<script>
import axios from 'axios';
import Home from './Home-Top.vue';
export default {
  name: 'MainContent',
  data() {
    return {
      tweets: [],
      newTweet: '',
      newReply: '',
      user: 'John Doe', // Hardcoded user for simplicity; you can use dynamic user data
    };
  },
  components: {
    Home
  },
  created() {
    this.fetchTweets();
  },
  methods: {
    fetchTweets() {
      axios.get('http://localhost:3000/tweets')
        .then(response => {
          this.tweets = response.data;
          console.log(this.tweets); // Log the fetched tweets to the console
        })
        .catch(error => {
          console.error('Error fetching tweets:', error);
        });
    },
    addTweet() {
      if (this.newTweet.trim() === '') return;

      const tweet = {
        content: this.newTweet,
        likes: 0,
        retweets: 0,
        liked: false, // Initialize with not liked
        retweeted: false, // Initialize with not retweeted
        replies: [], // Initialize with an empty array of replies
        showReplyBox: false, // Initialize with the reply box hidden
        user: this.user,
        created_at: new Date().toISOString(), // Current date and time
        id: this.uniqueId = this._uid, // Ensure a unique ID
      };

      axios.post('http://localhost:3000/tweets', tweet)
        .then(response => {
          this.tweets.push(response.data);
          this.newTweet = ''; // Clear the input field
          console.log(this.tweets); // Log the updated tweets array to the console
        })
        .catch(error => {
          console.error('Error adding tweet:', error);
        });
    },
    toggleLike(tweetId) {
      const tweet = this.tweets.find(t => t.id === tweetId);
      if (tweet) {
        tweet.liked = !tweet.liked;
        tweet.likes += tweet.liked ? 1 : -1;

        axios.put(`http://localhost:3000/tweets/${tweetId}`, tweet)
          .then(() => {
            this.$forceUpdate(); // Force Vue to re-render the component
            console.log(this.tweets); // Log the updated tweets array to the console
          })
          .catch(error => {
            console.error('Error updating tweet:', error);
          });
      }
    },
    toggleRetweet(tweetId) {
      const tweet = this.tweets.find(t => t.id === tweetId);
      if (tweet) {
        tweet.retweeted = !tweet.retweeted;
        tweet.retweets += tweet.retweeted ? 1 : -1;

        axios.put(`http://localhost:3000/tweets/${tweetId}`, tweet)
          .then(() => {
            this.$forceUpdate(); // Force Vue to re-render the component
            console.log(this.tweets); // Log the updated tweets array to the console
          })
          .catch(error => {
            console.error('Error updating tweet:', error);
          });
      }
    },
    toggleReplyBox(tweetId) {
      const tweet = this.tweets.find(t => t.id === tweetId);
      if (tweet) {
        tweet.showReplyBox = !tweet.showReplyBox;

        axios.put(`http://localhost:3000/tweets/${tweetId}`, tweet)
          .then(() => {
            this.$forceUpdate(); // Force Vue to re-render the component
            console.log(this.tweets); // Log the updated tweets array to the console
          })
          .catch(error => {
            console.error('Error updating tweet:', error);
          });
      }
    },
    addReply(tweetId) {
      const tweet = this.tweets.find(t => t.id === tweetId);
      if (tweet && this.newReply.trim() !== '') {
        const reply = {
          id: tweet.replies.length + 1,
          content: this.newReply
        };

        tweet.replies.push(reply);
        this.newReply = ''; // Clear the input field

        axios.put(`http://localhost:3000/tweets/${tweetId}`, tweet)
          .then(() => {
            this.$forceUpdate(); // Force Vue to re-render the component
            console.log(this.tweets); // Log the updated tweets array to the console
          })
          .catch(error => {
            console.error('Error adding reply:', error);
          });
      }
    },
    formatDate(date) {
      const options = { year: 'numeric', month: 'short', day: 'numeric', hour: '2-digit', minute: '2-digit' };
      return new Date(date).toLocaleDateString('en-US', options);
    }
  }
}
</script>
