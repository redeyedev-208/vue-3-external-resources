<template>
  <ul></ul>
</template>

<script>
export default {
  data() {
    storedResources: [
      {
        id: 'vue-3-official-guide',
        title: 'Official Guide',
        description: 'The official Vue.js (Vue 3) documentation',
        link: 'https://vuejs.org',
      },
      {
        id: 'google',
        title: 'Google',
        description: 'Learn to google...',
        link: 'https://google.org',
      },
    ];
  },
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
