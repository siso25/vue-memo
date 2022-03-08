<template>
  <textarea v-model="post.body"></textarea>
  <button @click="savePost">編集</button>
  <button @click="deletePost">削除</button>
</template>

<script>
export default {
  props: {
    paramPost: Object
  },
  emits: [
    'memo-save-click',
    'memo-delete-click'
  ],
  data () {
    return {
      post: this.paramPost
    }
  },
  methods: {
    savePost () {
      this.post.title = this.post.body.split('\n')[0]
      this.$emit('memo-save-click', this.post)
    },
    deletePost () {
      this.$emit('memo-delete-click', this.post)
    }
  }
}
</script>