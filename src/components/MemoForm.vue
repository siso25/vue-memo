<template>
  <textarea class="textarea" v-model="post.body"></textarea>
  <div class="mt-3">
    <button class="button" @click="savePost">編集</button>
    <button class="button ml-3" @click="deletePost">削除</button>
  </div>
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
