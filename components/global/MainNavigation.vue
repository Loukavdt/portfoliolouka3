<template>
  <div>
    <div v-for="(posts, foldername) in folders" :key="foldername" class="">
      <!-- Special Links Section: Contact and About Me -->
      <div class="special-links" v-if="hasSpecialPosts(posts)">
        <ul>
          <li
            v-for="post in posts.filter(shouldGroupPost)"
            :key="post.slug"
            class="pb-1 md:pb-2 lg:pb-3"
          >
            <NuxtLink :to="post._path" class="font-bold text-2xl lg:text-5xl xl:text-5xl">
              {{ post.title }}
            </NuxtLink>
          </li>
        </ul>
      </div>

      <!-- Regular Posts Section -->
      <ul>
        <li
          v-for="post in posts.filter(post => !shouldGroupPost(post))"
          :key="post.slug"
          class="pb-1 md:pb-2 lg:pb-3"
        >
          <NuxtLink :to="post._path" class="font-bold text-2xl lg:text-5xl xl:text-5xl">
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
const { data: foldersPosts } = await useAsyncData('folders', () =>
  queryContent('/')
    .sort({ numbernavigation: 1 })
    .find()
);

// Combine and filter the data
onMounted(() => {
  const allPosts = [...(foldersPosts.value || [])];
  if (allPosts.length) {
    folders.value = allPosts.filter(
      post => post.included && post.included === true && post.included !== false
    );
  }
});

// Helper Methods
function shouldGroupPost(post) {
  // Check if post is "Contact" or "About Me"
  return post.title === 'Contact' || post.title === 'About Me';
}

function hasSpecialPosts(posts) {
  // Check if any posts in the folder are "Contact" or "About Me"
  return posts.some(post => shouldGroupPost(post));
}
</script>

<style scoped>
.special-links {
  background-color: aqua;
  padding: 1rem;
  margin-bottom: 1rem;
}
</style>
