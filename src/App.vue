<script setup>
import { onMounted, ref } from 'vue'
import Account from './components/Account.vue';
import Auth from './components/Auth.vue';
import { supabase } from './clients/supabase';

const session = ref()

onMounted(() => {
  supabase.auth.getSession().then(({ data }) => {
    session.value = data.session
  })

  supabase.auth.onAuthStateChange((_, _session) => {
    session.value = _session
  })
})
</script>

<template>
  <!-- <div class="">
    <div class="px-14 flex justify-between py-7">
      <h1 class="text-white text-2xl font-bold">UserHub</h1>
      <button class="text-white">Sign up</button>
    </div>
  </div> -->
  <div class="container" style="padding: 50px 0 100px 0">
    <Account v-if="session" :session="session" />
    <Auth v-else />
  </div>
</template>


