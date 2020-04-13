<template>
  <div class="post">
    <b-container v-if="!  loading" text-align="center">
      <b-row>
        <h2 text-align="center">
          {{postSolo.title}}
          <b-badge>New</b-badge>
        </h2>
      </b-row>
      <b-row>
        <b-card>
          <b-card-body class="text-center">
            <b-card-title>Write by: {{user.name}}</b-card-title>

            <b-card-text>{{postSolo.body}}</b-card-text>

            <router-link to="/posts">
              <b-button variant="primary">Atrás</b-button>
            </router-link>
          </b-card-body>
        </b-card>
      </b-row>
    </b-container>
    <b-container v-else class="mb-5">
      <div class="text-center">
        <b-spinner label="Spinning"></b-spinner>
      </div>
    </b-container>
  </div>
</template>

<script>
const axios = require("axios");

export default {
  name: "Post",
  data() {
    return {
      postSolo: {},
      user: {},
      loading: true
    };
  },
  methods: {
    getPostSolo() {
      axios
        .get(
          `https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`,
          {}
        )
        .then(res => {
          this.postSolo = res.data;
          this.getPostUser(this.postSolo.userId);
        })
        .catch(err => {
          console.log(err);
        });
    },
    getPostUser(gfdgdfg) {
      axios
        .get(`https://jsonplaceholder.typicode.com/users/${gfdgdfg}`, {})
        .then(res => {
          this.user = res.data;
          this.loading = false;
        })
        .catch(err => {
          console.log(err);
        });
    }
  },
  created() {
    this.getPostSolo();
  }
};
</script>
