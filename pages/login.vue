<template>
  <div>
    <h2 class="login__title text-center">Login</h2>
    <div v-if="showError" class="max-w login__error-msg">
      <p>{{ errorMsg }}</p>
    </div>
    <form class="form max-w" @submit.prevent="logIn">
      <div class="form__group">
        <label class="form__label">Email</label>
        <input v-model="email" type="text" class="form__input" />
      </div>
      <div class="form__group">
        <label class="form__label">Password</label>
        <input v-model="password" type="password" class="form__input" />
      </div>
      <div class="form__group text-center">
        <button :disabled="loading" type="submit" class="form__btn">
          {{ loading ? 'Loading...' : 'Log in' }}
        </button>
      </div>
    </form>
    <div class="max-w text-center account-info">
      <p>
        Don't have an account?
        <NuxtLink class="account-info__link" to="/register"
          >Register here</NuxtLink
        >
      </p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ApiError } from '@supabase/gotrue-js';
const client = useSupabaseClient();
const email = ref('');
const password = ref('');
const loading = ref(false);
const showError = ref(false);
const errorMsg = ref('');
const logIn = async () => {
  try {
    loading.value = true;
    const { session, error } = await client.auth.signIn({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
    // Make sure the session is set before the `auth` middleware runs
    await client.auth.setSession(session.refresh_token);
    navigateTo('/profile');
  } catch (e) {
    const error = e as ApiError;
    showError.value = true;
    errorMsg.value = error.message;
  } finally {
    loading.value = false;
  }
};
useHead({
  title: 'Login Page',
  meta: [{ name: 'description', content: 'Login Page description' }],
  bodyAttrs: {
    class: 'login-page',
  },
});
</script>
