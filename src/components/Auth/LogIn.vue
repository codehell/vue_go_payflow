<template>
  <div class="max-w-xs mx-auto">
    Log In
    <form @submit.prevent="signIn">
      <div>
        Username
        <input class="bg-gray-200" type="text" name="username" v-model="username" />
      </div>
      <div class="mt-4">
        Email
        <input class="bg-gray-200" type="text" name="email" v-model="email" />
      </div>
      <br />
      <button class="mt-4" type="submit">Send</button>
    </form>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class LogIn extends Vue {
  username: string = '';
  email: string = '';
  csrf: string = '';

  async mounted() {
    const request = new Request('/api/crsf', { method: 'GET' });
    const response = await fetch(request);
    let resToken: string | null;
    resToken = response.headers.get('x-crsf-token');
    this.csrf = resToken ? resToken : '';
  }

  async login() {
    const response = await fetch('/api/users', {
      method: 'POST',
      headers: {
        'X-CSRF-Token': this.csrf,
      },
      body: JSON.stringify({
        username: this.username,
        email: this.email,
      }),
    });
  }
}
</script>
