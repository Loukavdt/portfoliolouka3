<template>
  <div>
    <div v-for="(posts, foldername) in folders" :key="foldername" class="">
    <ul>
      <li v-for="post in posts" :key="post.slug" class="pb-1 md:pb-2 lg:pb-3">
        <NuxtLink 
          :to="post._path" >
          class="font-bold text-2xl lg:text-5xl xl:text-5xl"
          
        {{ post.title }}
      </NuxtLink>
      </li>
    </ul>
    </div>
  </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { useAsyncData } from '#app';
  
  // Define a ref for storing folders
  const folders = ref([]);
  
  // Fetch all posts from both /folders and /page
  const { data: foldersPosts } = await useAsyncData('folders', () => queryContent('/')
  .sort({ numbernavigation: 1 })
  .find());

  // Combine and filter the data
  onMounted(() => {
    const allPosts = [...(foldersPosts.value || [])];
    if (allPosts.length) {
      folders.value = allPosts.filter(post => post.included && post.included === true && post.included !== false);
    }
  });
  </script>
