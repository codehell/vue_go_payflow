<template>
    <div class="hello">
        Restaurants
        <ul>
            <li v-for="(restaurant, key) in restaurants" :key="key">{{restaurant.name}}</li>
        </ul>
    </div>
</template>

<script lang="ts">
    import {Component, Prop, Vue} from 'vue-property-decorator';

    @Component
    export default class HelloWorld extends Vue {
        restaurants = [];
        @Prop() private msg!: string;

        async mounted() {
            let token: string = '';
            const request = new Request('/api/crsf', {method: 'GET'});
            const response = await fetch(request);
            let resToken: string | null;
            resToken = response.headers.get('x-crsf-token');
            token = resToken ? resToken : '';

            const rRes = await fetch('/api/restaurants', {
                method: 'GET',
                headers: {
                    'Accept': 'application/json',
                    'X-CSRF-Token': token,
                },
            });
            rRes.json().then((jsonRRes) => {
                this.restaurants = jsonRRes;
            });
        }
    }
</script>
