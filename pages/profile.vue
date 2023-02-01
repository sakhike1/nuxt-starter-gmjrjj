<template>
  <div class="container">
    <h1>Profile</h1>
    <p class="mt-8 mb-16">Hello {{ user.email }}</p>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  middleware: ['auth'],
});
const user = useSupabaseUser();
useHead({
  title: 'My Profile',
  meta: [{ name: 'description', content: 'My amazing site.' }],
  bodyAttrs: {
    class: 'profile',
  },
});
</script>
