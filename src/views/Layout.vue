<script setup>
  import TopNav from '@/components/TopNav.vue';
  import SideNav from '@/components/SideNav.vue';
  import { authStore } from '@/store/auth';
  import { apiCheckSignin } from '@/apis/metawall.js';
  import { useRouter } from 'vue-router';

  const auth = authStore();
  const router = useRouter();
  
  apiCheckSignin().then((res) => {
    if (res.data.status) {
      auth.user = res.data.data
    }
  }).catch(() => {
    router.replace({ name: 'signin' });
  }) 
</script>

<template>
  <div class="container-fluid bg-white border-bottom border-dark border-2">
    <TopNav/>
  </div>
  <div class="container pt-12">
    <div class="row">
      <div class="col-md-8">
        <router-view/>
      </div>
      <div class="col-md-4">
        <SideNav/>
      </div>
    </div>
  </div>
  
</template>

<style lang="scss">

</style>
