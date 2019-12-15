<template>
  <div class="hello mt-3">
    <ul class="list-unstyled">
      <li v-for="post in posts" class="media m-3">
        <img :src="post.data.thumbnail" class="mr-3" alt="">
        <div class="media-body">
          <h5 class="mt-0 mb-1"><a href="createUrl(post.data.permalink)" target="_blank">{{ post.data.title }}</a></h5>
          <p>
            <h3 class="text-danger">{{ post.data.ups }} 👆</h3>
            <p>created {{ post.data.created }} ago by {{ post.data.author }}</p>
            <span class="badge badge-pill badge-primary">{{ post.data.num_comments }} comments</span>
            <button 
              v-if="isImage(post)"
              @click="post.showImage = !post.showImage" 
              type="button" 
              class="btn btn-primary">
              {{ post.showImage ? 'Hide' : 'Show' }} Image
            </button>
            <div v-if="post.showImage">
              <img :src="post.data.url" alt="">
            </div>
          </p>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { parse, distanceInWords } from 'date-fns'
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
          result.data.children.forEach(child => {
            child.showImage = false;
          });
          this.posts = result.data.children;
        });
    },
    createUrl(path) {
      return `https://www.reddit.com${path}`
    },
    isImage(post) {
      return post.data.url.match(/\.(jpg|png|jpeg|bpm)$/)
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
