<template>
  <div class="posts">
    <div class="overflow-auto">
      <b-container v-if="images.length > 0" class="mb-5">
        <b-row>
          <b-card-group columns>
            <PostCard
              v-for="(post, index) of postsPagination"
              :key="index"
              :post="post"
              :image="images[post.id]"
            ></PostCard>
          </b-card-group>
        </b-row>

        <b-row>
          <b-col>
            <b-pagination
              v-model="currentPage"
              :total-rows="rows"
              :per-page="perPage"
              aria-controls="my-table"
              align="center"
            ></b-pagination>
          </b-col>
        </b-row>
      </b-container>

      <b-container v-else class="mb-5">
        <div class="text-center">
          <b-spinner label="Spinning"></b-spinner>
        </div>
      </b-container>
    </div>
  </div>
</template>

<script>
import PostCard from "@/components/PostCard.vue";

const axios = require("axios");

export default {
  name: "Posts",
  data() {
    return {
      perPage: 9,
      currentPage: 1,
      posts: [],
      images: []
    };
  },
  components: {
    PostCard
  },
  computed: {
    rows() {
      return this.posts.length;
    },
    postsPagination() {
      return this.posts.slice(
        this.currentPage * this.perPage,
        this.currentPage * this.perPage + this.perPage
      );
    }
  },
  methods: {
    getPosts() {
      axios
        .get("https://jsonplaceholder.typicode.com/posts", {})
        .then(res => {
          this.posts = res.data;
        })
        .catch(err => {
          console.log(err);
        });
    },
    getImages() {
      axios
        .get("https://jsonplaceholder.typicode.com/photos", {})
        .then(res => {
          this.images = res.data;
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
