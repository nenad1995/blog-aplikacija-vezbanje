<template>
  <div>
    <form @submit.prevent="onSubmit"> 
      <div>
        <label>Naslov</label>
        <br />
        <input v-model="post.title" />
      </div>
      <hr />
      <div>
        <label>Tekst</label>
        <br />
        <input v-model="post.text" />
      </div>
      <hr />
      <div>
        <button type="submit">
          Postavi novi post
        </button>
      </div>
    </form>
  </div>
</template>

<script>
import { postsService } from '../services/Posts'

export default {
  data() {
    return {
      post: {
        title: '',
        text: ''
      }
    }
  },

  methods: {
    onSubmit() {
      postsService.add(this.post)
        .then(response => {
          this.$router.push({ name: 'posts' })
        })
        .catch(e => {
          alert(e)
        })
    }
  }
}
</script>
