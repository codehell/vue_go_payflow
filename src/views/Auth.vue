<template>
  <div>
    <SignIn/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import SignIn from '@/components/Auth/SignIn.vue';

@Component({
  components: {
    SignIn,
  },
})
export default class Auth extends Vue {}
</script>
