<template>
  <main class="w-1/2 p-4">
    <Home />
    <div class="bg-white p-4 rounded-lg shadow mb-4">
      <form @submit.prevent="addTweet" class="flex space-x-4">
        <img src="user-avatar.png" alt="User Avatar" class="h-10 w-10 rounded-full">
        <input v-model="newTweet" type="text" placeholder="What's happening?" class="flex-1 p-2 border rounded-lg" required />
        <button type="submit" class="bg-blue-500 text-white py-2 px-4 rounded-full">Tweet</button>
      </form>
    </div>
    <ul class="space-y-4">
      <li v-for="tweet in tweets" :key="tweet.id" class="bg-white p-4 rounded-lg shadow border-b border-gray-300">
        <div class="flex space-x-4">
          <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRXJA32WU4rBpx7maglqeEtt3ot1tPIRWptxA&s" alt="User Avatar" class="h-10 w-10 rounded-full">
          <div>
            <div class="text-gray-900">{{ tweet.content }}</div>
            <div class="flex space-x-2 text-gray-500 text-sm mt-2">
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

export default {
  name: 'MainContent',
  data() {
    return {
      tweets: [],
      newTweet: '',
      newReply: ''
    };
  },
  created() {
    this.fetchTweets();
  },
  methods: {
    fetchTweets() {
      axios.get('http://localhost:3000/tweets')
        .then(response => {
          this.tweets = response.data.map(tweet => ({
            ...tweet,
            replies: tweet.replies || [],
            showReplyBox: false,
          }));
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
        id: String( this.tweets.length + 1), // Ensure a unique ID

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
        this.$forceUpdate(); // Force Vue to re-render the component
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
    }
  }
}
</script>
