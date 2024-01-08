<template>
  <UCard class="shadow-xl text-center bg-slate-200">
    Home Page
  </UCard>
</template>
<script lang="ts" setup>
import { storeToRefs } from "pinia";
import { useAuthStore } from "~/store/auth";
const { authenticated } = storeToRefs(useAuthStore()); // make authenticated state reactive
const token = useCookie('secretStore'); // get token from cookies

  if (token.value) {
    // check if value exists
    authenticated.value = true; // update the state to authenticated
  }

</script>