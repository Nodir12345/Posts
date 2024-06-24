<template>
  <div>
    <h1>Blog Posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.id">
        <NuxtLink :to="`/post/${post.id}`">{{ post.title }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const posts = ref([]);

onMounted(async () => {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts');
  posts.value = await response.json();
});
</script>
