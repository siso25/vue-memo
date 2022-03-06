<template>
  <ul>
    <li v-for="post in posts" :key="post.id">
      {{ post.title }}
    </li>
    <li @click="$emit('new-button-click')">+</li>
  </ul>
</template>

<script>
export default {
  props: {
    posts: Array
  },
  emits: ['new-button-click']
}
</script>
