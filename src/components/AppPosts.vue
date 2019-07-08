<template>
  <div>
    <div v-for="(post, index) in posts" :key="post.id">
      <h3>{{ post.title }}</h3>
      <div>{{ post.text }}</div>
      <div>{{ post.createdAt | formatDate }}</div>
      <div>
        <router-link :to="{ name: 'view', params: { id: post.id } }">
          View Post
        </router-link>
        <router-link :to="{ name: 'edit', params: { id: post.id } }">
          Edit Post
        </router-link>
        <div>
          <button @click="deletePost(post.id, index)">
            Delete Post
          </button>
        </div>
        <div>
          <span>Number of comments: {{ post.comments.length }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { postsService } from '../services/Posts'
import { DateMixin } from '../mixins'

export default {
  data() {
    return {
      posts: []
    }
  },

  mixins: [ DateMixin ],
  
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
  },

  methods: {
    deletePost(id, index) {
      postsService.delete(id)
        .then(response => {
          this.posts.splice(index, 1)
        })
        .catch(e => {
          alert(e)
        })
    }
  }
}
</script>
