<template>
  <div class="home">
    <h1>Welcome to Our Forum</h1>
    <div v-for="thread in threads" :key="thread.id" class="thread">
      <h2>{{ thread.title }}</h2>
      <div v-for="postId in thread.posts" :key="postId" class="post">
        <div class="user-info">
          <img src="../assets/avatar.png" alt="User Avatar" class="avatar" />
          <p class="username">{{ getUserByPostId(postId).name }}</p>
        </div>
        <p class="post-text">{{ getPostTextById(postId).text }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import sourceData from '../data.json';
import { ref } from 'vue';

const threads = ref(sourceData.threads)
const posts = ref(sourceData.posts)
const users = ref(sourceData.users)

function getUserByPostId(postId) {
  const post = posts.value.find(post => post.id === postId);
  const user = users.value.find(user => user.id === post.userId);
  return user;
}

function getPostTextById(postId) {
  return posts.value.find(post => post.id === postId);
}
</script>

<style scoped>
.home {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
  }

  .thread {
    margin-bottom: 30px;
    border-bottom: 1px solid #ccc;
    padding-bottom: 20px;
  }

  .thread h2 {
    color: #333;
    font-size: 24px;
  }

  .post {
    display: flex;
    align-items: flex-start;
    margin-top: 15px;
  }

  .user-info {
    margin-right: 15px;
  }

  .avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
  }

  .username {
    font-weight: bold;
    margin-top: 5px;
  }

  .post-text {
    font-size: 16px;
    line-height: 1.5;
    color: #555;
  }
</style>
