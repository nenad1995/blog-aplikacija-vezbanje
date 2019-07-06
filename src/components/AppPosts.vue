<template>
  <div>
    <div v-for="post in posts" :key="post.id">
      <h3>{{ post.title }}</h3>
      <div>{{ post.text }}</div>
      <div>{{ post.createdAt }}</div>
    </div>
  </div>
</template>

<script>
import { postsService } from '../services/Posts'

export default {
  data() {
    return {
      posts: []
    }
  },

  created() {
    postsService.getAll()
      .then(response => {
        this.posts = response.data
      })
      .catch(e => {
        alert(e)
      })
  }
}
</script>
