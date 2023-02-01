<template>
  <div class="container">
    <h2>About Page</h2>
    <p>
      Lorem, ipsum dolor sit amet consectetur adipisicing elit. Eveniet rerum
      quos et!
    </p>
  </div>
</template>
<script setup lang="ts">
definePageMeta({
  middleware: ['auth'],
});
</script>
