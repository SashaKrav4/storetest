<template>
  <div class="flex flex-col h-screen">
    <header class="w-full flex justify-between mb-5">

      <NuxtLink class="mr-5 no-underline block mt-4  text-gray-700 hover:text-gray-400" to="/">
        Home</NuxtLink>
      <NuxtLink class="mr-5 no-underline block mt-4  text-gray-700 hover:text-gray-400" to="/about">
        About</NuxtLink>
      <UButton v-if="!authenticated" class="mr-5 no-underline block mt-4  text-gray-700 hover:text-gray-400 " to="/login">
        Login</UButton>
      <UButton v-else class="mr-5 no-underline block mt-4  text-gray-700 hover:text-gray-400" @click="logout">
        Logout</UButton>
    </header>

    <div class="flex justify-center mt-auto">
      <slot />
    </div>
    <footer class='bg-slate-200 mt-auto'>
      <h1>Footer @Copyright</h1>
    </footer>
  </div>
</template>
<script lang="ts" setup>
import { storeToRefs } from 'pinia'; // import storeToRefs helper hook from pinia
import { useAuthStore } from '~/store/auth'; // import the auth store we just created

const router = useRouter();
const { logUserOut } = useAuthStore(); // use authenticateUser action from  auth store
const { authenticated } = storeToRefs(useAuthStore()); // make authenticated state reactive with storeToRefs

const logout = () => {
  logUserOut();
  router.push('/login');
};
</script>