<template>
  <textarea v-model="post.body"></textarea>
  <p>{{ post.body }}</p>
  <button @click="saveBody">{{ buttonName }}</button>
</template>

<script>
export default {
  props: {
    paramPost: Object,
    buttonName: String
  },
  emits: ['memo-form-save'],
  data () {
    return {
      post: this.paramPost
    }
  },
  methods: {
    saveBody () {
      this.post.title = this.post.body.split('\n')[0]
      this.$emit('memo-form-save', this.post)
    }
  }
}
</script>