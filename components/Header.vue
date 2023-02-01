<template>
  <header class="header">
    <div class="flex container">
      <NuxtLink to="/">Home</NuxtLink>
      <nav v-if="user" class="header__nav">
        <NuxtLink to="/about" class="header__link"> About </NuxtLink>
        <NuxtLink to="/profile" class="header__link"> Profile </NuxtLink>
        <button class="header__btn logout" @click="handleLogOut">
          Log out
        </button>
      </nav>
      <nav v-else class="header__nav">
        <NuxtLink to="/login" class="header__btn login"> Log in </NuxtLink>
        <NuxtLink to="/register" class="header__btn register">
          Register
        </NuxtLink>
      </nav>
    </div>
  </header>
</template>

<script setup lang="ts">
const user = useSupabaseUser();
const client = useSupabaseClient();
const handleLogOut = async () => {
  await client.auth.signOut();
  navigateTo('/login');
};
</script>
