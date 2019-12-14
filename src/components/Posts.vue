<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li class="media">
        <img src="">
        <div class="media-body">
          <h5 class="mt-0 mb-1">List-based media object</h5>
          Cras sit amet nibh libero, in gravida nulla. Nulla vel metus scelerisque ante sollicitudin. Cras purus odio, vestibulum in vulputate at, tempus viverra turpis. Fusce condimentum nunc ac nisi vulputate fringilla. Donec lacinia congue felis in faucibus.
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Posts',
  data() {
    return {
      posts: [],
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
