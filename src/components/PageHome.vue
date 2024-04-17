<template>
  <div>
    <!-- Your component content here -->
    <h1>Welcome to Home Page</h1>
    <p>This is the home page of your Vue forum.</p>
    <div v-for="thread in threads" :key="thread.id">
      <h2>{{ thread.title }}</h2>
      <div v-for="postId in thread.posts" :key="postId">

        <!-- <p>{{ users.find(u => u.id === posts.find(p => p.id === postId).userId).name }}</p>
        <p>{{ posts.find(p => p.id === postId).text }}</p> -->

        <!-- If not using the methods, use it -->
        <p>{{ getUserByPostId(postId).name }}</p>
        <p>{{ getPostTextById(postId).text }}</p>

      </div>
    </div>
  </div>
</template>

<script>
import sourceData from '../data.json';

export default {
  // Component options here
  data() {
    return {
      threads: sourceData.threads,
      posts: sourceData.posts,
      users: sourceData.users,
    };
  },

  methods: {
    getUserByPostId(postId) {
      const userId = this.posts.find(post => post.id === postId).userId;
      return this.users.find(user => user.id === userId);
    },
    getPostTextById(postId) {
      return this.posts.find(post => post.id === postId);
    }
  }

};
</script>

<style scoped>
/* Component styles here */
</style>
