<template>
  <div class="slider-posts">
    <b-container class="mb-5">
      <b-row class="justify-content-center">
        <b-col col lg="6" md="6" sm="10">
          <b-carousel
            v-if="images.length > 0"
            id="carousel-fade"
            style="text-shadow: 0px 0px 2px #000"
            fade
            indicators
          >
            <b-carousel-slide
              v-for="(post, index) of posts"
              :key="index"
              :img-src="images[index].url"
              :caption="post.title"
            ></b-carousel-slide>
          </b-carousel>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  name: "SliderPosts",
  data() {
    return {
      posts: [],
      images: []
    };
  },
  methods: {
    getPosts() {
      axios
        .get("https://jsonplaceholder.typicode.com/posts", {})
        .then(res => {
          const inicio = Math.floor(Math.random() * (97 + 1 - 1) + 1);

          this.posts = res.data.splice(inicio, 3);
        })
        .catch(err => {
          console.log(err);
        });
    },
    getImages() {
      axios
        .get("https://jsonplaceholder.typicode.com/photos", {})
        .then(res => {
          const inicio = Math.floor(Math.random() * (4997 + 1 - 1) + 1);

          this.images = res.data.splice(inicio, 3);
        })
        .catch(err => {
          console.log(err);
        });
    }
  },

  created() {
    this.getPosts();
    this.getImages();
  }
};
</script>
