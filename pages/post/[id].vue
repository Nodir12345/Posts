<template>
  <div>
    <h1>{{ post.title }}</h1>
    <p><strong>Author:</strong> {{ author.name }}</p>
    <p>{{ post.body }}</p>
    <NuxtLink to="/">Back to posts</NuxtLink>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';


const post = ref({});
const author = ref({});
const route = useRoute();

// posIdni asinxron qilib route orqali posIddan

onMounted(async () => {
  const postId = route.params.id;
  const postResponse = await fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`);
  post.value = await postResponse.json();
// userIDni  asinxron qilib route orqali posni valuesini userIdsidan
  const authorResponse = await fetch(`https://jsonplaceholder.typicode.com/users/${post.value.userId}`);
  author.value = await authorResponse.json();
});


</script>
