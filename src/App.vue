<template>
  <div>
    <HeaderSet />
  </div>
</template>

<script>
import HeaderSet from './views/HeaderSet.vue'
import { createClient, provideClient } from '@urql/vue';
export default {
  components: {
    HeaderSet
  },
  setup() {
    const client = createClient({
      url: 'http://38.242.229.113:8055/graphql'
      // url: 'http://localhost:1337/graphql'
    });
    provideClient(client)
  }
}
</script>

<style>
</style>
