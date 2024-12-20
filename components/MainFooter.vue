<template>
    <div class="w-full bg-[#000] mt-16 z-100">
      <div class="p-16 flex justify-evenly flex-wrap gap-10">
        <!-- Portfolio Section -->
        <div class="footer-item text-center">
          <p>Thank you for reviewing my</p>
          <h1 class="text-3xl mt-2">Portfolio</h1>
        </div>
  
        <!-- Contact Me Section -->
        <div class="footer-item text-center">
          <h1 class="text-xl">Contact Me</h1>
          <div class="flex justify-center space-x-4 mt-4">
            <!-- Email Link -->
            <NuxtLink
              to="mailto:loukavdt2002@gmail.com?subject=Hello%20Louka&body=This%20is%20a%20test%20email!"
              class="border border-black hover:border-white hover:text-white transition-all duration-100 rounded-full px-4 py-2 text-sm"
            >
              Email
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  </script>
  
  <style scoped>
  .footer-item {
    width: 250px;
  }
  </style>
  