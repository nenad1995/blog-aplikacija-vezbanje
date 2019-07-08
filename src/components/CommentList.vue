<template>
  <div>
    <li v-for="comment in comments" :key="comment.id">
      {{ comment.text }} - {{ comment.createdAt | diffForHumans }}

    </li>
  </div>
</template>

<script>
import { DateMixin } from '../mixins'

export default {
  props: {
    comments: Array
  },

  mixins: [ DateMixin ]
}
</script>
