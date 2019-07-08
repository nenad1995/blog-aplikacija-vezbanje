<template>
  <div>
    <li v-for="comment in comments" :key="comment.id">
      {{ comment.text }}
    </li>
  </div>
</template>

<script>
export default {
  props: {
    comments: Array
  }
}
</script>
