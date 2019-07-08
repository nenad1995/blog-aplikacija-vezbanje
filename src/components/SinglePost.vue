<template>
  <div>
    <h3>{{ post.title }}</h3>
    <div>{{ post.text }}</div>
    <div>{{ post.createdAt | formatDate }}</div>
    <add-comment @commentAdded="addComment"></add-comment>
    <comment-list :comments="comments"></comment-list>
  </div>
</template>

<script>
import { postsService } from '../services/Posts'
import AddComment from './AddComment.vue'
import CommentList from './CommentList.vue'
import { DateMixin } from '../mixins'

export default {
  components: {
    AddComment,
    CommentList
  },

  data() {
    return {
      post: {}
    }
  },

  mixins: [ DateMixin ],

  methods: {
    addComment(comment) {
      postsService.addComment(comment, this.post.id)
        .then(response => {
          postsService.get(this.post.id)
            .then(response => {
              this.post = response.data
            })
            .catch(e => {
              alert(e)
            })
        }).catch(e => {
          alert(e)
        })
    }
  },

  computed: {
    comments() {
      return this.post.comments
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