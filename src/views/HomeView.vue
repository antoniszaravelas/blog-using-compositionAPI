<template>
  <h1>Hello People! That's the home of {{ name }}:D</h1>
  <h3>My Posts:</h3>
  <Posts />
</template>

<script>
import { ref } from 'vue';
import Posts from '../components/Posts.vue';

export default {
  name: 'HomeView',
  components: { Posts },
  setup() {
    const name = ref('antonis');

    return { name };
  },
};
</script>
