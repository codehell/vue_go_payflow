<template>
  <div>
    <form @submit.prevent="signIn">
      Username <input type="text" name="username" v-model="username"> <br>
      Email <input type="text" name="email" v-model="email"> <br>
      <button type="submit">Send</button>
    </form>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';

@Component
export default class SignIn extends Vue {
  username: string = '';
  email: string = '';
  csrf: string = '';

  async mounted() {
    const request = new Request('/api/crsf', { method: 'GET' });
    const response = await fetch(request);
    let resToken: string|null;
    resToken = response.headers.get('x-crsf-token');
    this.csrf = resToken ? resToken : '';
  }

  async signIn() {
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
