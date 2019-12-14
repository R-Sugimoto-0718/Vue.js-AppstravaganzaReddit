<template>
  <div class="hello">
    <h1>posts</h1>
  </div>
</template>

<script>
export default {
  name: 'Posts',
  data() {
    return {
      posts: []
    };
  },
  mounted() {
    this.load();
  },
  methods: {
    load() {
      // fetch the post
      const url = 'https://www.reddit.com/r/rarepuppers/.json';
      fetch(url)
        .then(res => res.json())
        .then((result) => {
          this.posts = result.data.children;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
