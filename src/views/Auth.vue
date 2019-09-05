<template>
  <div>
    <router-view />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SignIn from '@/components/Auth/SignIn.vue';

@Component
export default class Auth extends Vue { }
</script>
