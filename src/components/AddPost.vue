<template>
  <div>
    <form @submit.prevent="onSubmit" @reset="reset"> 
      <div>
        <label>Naslov</label>
        <input required="required" minlength="2" v-model="post.title" />
      </div>
      <hr />
      <div>
        <label>Tekst</label>
        <input required="required" maxlength="300" v-model="post.text" />
      </div>
      <hr />
      <div>
        <button type="submit">
          {{ editable ? "Edit" : "Submit" }}
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
      },

      editable: false
    }
  },

  beforeRouteEnter(to, from, next) {
    next(vm => {
      if(vm.$route.params.id) {
        vm.editable = true
        postsService.get(vm.$route.params.id)
          .then(response => {
            vm.post = response.data
          })
      }
    })  
  },

  methods: {
    onSubmit() {
      if(this.$route.params.id) {
        this.editPost()
      } else {
        this.addPost()
      }
    },

    addPost() {
      postsService.add(this.post)
        .then(response => {
          this.$router.push({ name: 'posts' })
        })
        .catch(e => {
          alert(e)
        })
    },

    editPost() {
      postsService.update(this.post)
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
