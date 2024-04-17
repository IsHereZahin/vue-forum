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

        <!-- If not using the functions, use it -->
        <p>{{ getUserByPostId(postId).name }}</p>
        <p>{{ getPostTextById(postId).text }}</p>

      </div>
    </div>
  </div>
</template>

<script setup>
import sourceData from '../data.json';
// import { reactive } from 'vue';
// const threads = reactive(sourceData.threads)
// const posts   = reactive(sourceData.posts)
// const users   = reactive(sourceData.users)

import { ref } from 'vue';

const threads = ref(sourceData.threads)
const posts   = ref(sourceData.posts)
const users   = ref(sourceData.users)

function getUserByPostId(postId)
{
  const userId = this.posts.find(post => post.id === postId).userId;
  return users.value.find(user => user.id === userId);
}
function getPostTextById(postId)
{
  return posts.value.find(post => post.id === postId);
}

</script>

<style scoped>
/* Component styles here */
</style>
