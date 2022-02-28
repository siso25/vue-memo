<template>
  <ul>
    <li v-for="post in posts" :key="post.id">
      {{ post.text }}
    </li>
  </ul>
</template>

<script>
export default {
  name: 'MemoList',
  props: {
    posts: Array
  }
}
</script>
