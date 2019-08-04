<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Restaurants msg="Welcome to Your Vue.js + TypeScript App"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Restaurants from '@/components/Restaurants.vue'; // @ is an alias to /src

@Component({
  components: {
    Restaurants,
  },
})
export default class Home extends Vue {}
</script>
