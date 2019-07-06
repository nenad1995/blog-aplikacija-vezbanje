<template>
  <div>
    <h3>{{ post.title }}</h3>
    <div>{{ post.text }}</div>
    <div>{{ post.createdAt }}</div>
  </div>
</template>

<script>
import { postsService } from '../services/Posts'

export default {
  data() {
    return {
      post: {}
    }
  },

  beforeRouteEnter(to, from, next) {
    postsService.get(to.params.id)
      .then(response => {
        next(vm => {
          vm.post = response.data
        })
      })
      .catch(e => {
        alert(e)
      })
  }
}
</script>