<template>
  <form @submit.prevent="onSubmit">
    <div>
      <div>
        <textarea required="required" v-model="comment.text"></textarea>
      </div>
      <div>
        <button type="submit">
          Submit Comment
        </button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      comment: {
        text: ''
      }
    }
  },

  methods: {
    onSubmit() {
      this.$emit('commentAdded', this.comment)
    }
  }
}
</script>