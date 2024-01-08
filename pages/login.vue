<template>
  <UCard class="shadow-xl">

      <UFormGroup label="Login" name="uname">
        <UInput v-model="user.username" placeholder="Ivan" />
      </UFormGroup>

      <UFormGroup label="Password" name="password">
        <UInput v-model="user.password" type="password" placeholder="**********" />
      </UFormGroup>

    <template #footer>
        <UButton color="primary" variant="solid" label="Login" :trailing="false" type="submit" @click.prevent="login" />
    </template>
  </UCard>
</template>

  
<script lang="ts" setup>

definePageMeta({
  layout: 'login',
});

import { storeToRefs } from 'pinia'; // import storeToRefs helper hook from pinia
import { useAuthStore } from '~/store/auth'; // import the auth store we just created

const { authenticateUser } = useAuthStore(); // use authenticateUser action from  auth store

const { authenticated } = storeToRefs(useAuthStore()); // make authenticated state reactive with storeToRefs

const user = ref({
  username: 'kminchelle',
  password: '0lelplR',
});
const router = useRouter();

const login = async () => {
  await authenticateUser(user.value); // call authenticateUser and pass the user object
  // redirect to homepage if user is authenticated
  if (authenticated) {
    router.push('/');
  }
};
</script>