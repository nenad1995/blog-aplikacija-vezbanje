<template>
  <div>
    <form @submit.prevent="onSubmit" @reset="reset"> 
      <div>
        <label>Naslov</label>
        <br />
        <input required="required" minlength="2" v-model="post.title" />
      </div>
      <hr />
      <div>
        <label>Tekst</label>
        <br />
        <input required="required" maxlength="300" v-model="post.text" />
      </div>
      <hr />
      <div>
        <button type="submit">
          Postavi novi post
        </button>
        <button type="reset">
          Resetuj unos
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
    },

    reset() {
      this.post.title = ''
      this.post.text = ''
    }
  }
}
</script>
