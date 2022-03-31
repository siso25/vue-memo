<template>
  <ul class="mt-0">
    <li class="mb-2" v-for="post in posts" :key="post.id" @click="$emit('post-title-click', post)">
      <a>{{ post.title }}</a>
    </li>
    <li class="is-size-5" @click="$emit('new-button-click')"><a>+</a></li>
  </ul>
</template>

<script>
export default {
  props: {
    posts: Array
  },
  emits: [
    'new-button-click',
    'post-title-click'
  ]
}
</script>
