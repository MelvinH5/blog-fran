<template>
  <b-card
    :title="post.title"
    :img-src="image.url"
    img-alt="Image"
    img-top
    tag="article"
    style="width: 20rem;"
    class="mb-2"
  >
    <b-card-text>{{post.body}}</b-card-text>
    <router-link :to="{name:'Post', params:{id:post.id}}">
      <b-button variant="primary">Ver</b-button>
    </router-link>
  </b-card>
</template>

<script>
export default {
  name: "PostCard",
  props: ["post", "image"]
};
</script>
