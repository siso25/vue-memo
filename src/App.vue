<template>
  <div id="app">
    <div>
      <MemoList :posts="posts" @new-button-click="showNewMemoForm"/>
    </div>
    <div v-if="formShow">
      <MemoForm :button-name="buttonName" :param-post="post" @memo-form-save="save"/>
    </div>
  </div>
</template>

<script>
import MemoList from './components/MemoList.vue'
import MemoForm from './components/MemoForm.vue'

const STORAGE_KEY = 'vuejs-memo-app'

const fetchStorage = () => {
  const posts = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]')
  return posts
}

const saveStorage = (posts) => {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(posts))
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
      formShow: false,
      buttonName: ''
    }
  },
  created () {
    this.posts = fetchStorage()
  },
  methods: {
    showNewMemoForm() {
      this.buttonName = '新規作成'
      this.formShow = true
    },
    save(post) {
      if (!post.id) {
        post.id = this.createId()
        this.posts.push(post)
      } else {
        const targetIndex = this.posts.findIndex(item => item.id === post.id)
        this.posts.splice(targetIndex, 1, post)
      }

      saveStorage(this.posts)
      this.formShow = false
    },
    createId() {
      if (this.posts.length === 0) {
        return 1
      }
      const maxId = Math.max(...this.posts.map(post => post.id))
      return maxId + 1
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
