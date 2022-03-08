<template>
  <div id="app">
    <div>
      <MemoList :posts="posts" @new-button-click="showNewForm" @post-title-click="showEditForm"/>
    </div>
    <div v-if="formShow">
      <MemoForm :param-post="post" @memo-save-click="savePost" @memo-delete-click="deletePost"/>
    </div>
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'
import MemoForm from './components/MemoForm.vue'

const STORAGE_KEY = 'vuejs-memo-app'
const storage = {
  fetch: () => {
    const posts = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
    return posts
  },
  save: (posts) => {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(posts))
  }
}

export default {
  name: 'App',
  components: {
    MemoList,
    MemoForm
  },
  data () {
    return {
      posts: [],
      post: {},
      formShow: false
    }
  },
  created () {
    this.posts = storage.fetch()
  },
  methods: {
    showNewForm () {
      this.post = {}
      this.formShow = true
    },
    showEditForm (post) {
      this.post = post
      this.formShow = true
    },
    savePost (post) {
      if (!post.id) {
        post.id = this.createId()
        this.posts.push(post)
      } else {
        const targetIndex = this.posts.findIndex(item => item.id === post.id)
        this.posts.splice(targetIndex, 1, post)
      }

      storage.save(this.posts)
      this.formShow = false
    },
    createId () {
      if (this.posts.length === 0) {
        return 1
      }
      const maxId = Math.max(...this.posts.map(post => post.id))
      return maxId + 1
    },
    deletePost (post) {
      if (!post.id) {
        this.formShow = false
        return
      }

      this.posts = this.posts.filter(item => item.id !== post.id)
      storage.save(this.posts)
      this.formShow = false
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
