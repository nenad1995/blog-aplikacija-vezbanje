<template>
  <div>
    <div v-for="post in posts" :key="post.id">
      <h3>{{ post.title }}</h3>
      <div>{{ post.text }}</div>
      <div>{{ post.createdAt }}</div>
      <div>
        <router-link :to="{ name: 'view', params: { id: post.id } }">
          View Post
        </router-link>
        <router-link :to="{ name: 'edit', params: { id: post.id } }">
          Edit Post
        </router-link>
      </div>
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
  
  beforeRouteEnter(to, from, next) {
    postsService.getAll()
      .then(response => {
        next(vm => {
          vm.posts = response.data
        })
      })
      .catch(e => {
        alert(e)
      })
  }
}
</script>
