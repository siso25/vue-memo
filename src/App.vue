<template>
  <MemoList :posts="[{id:1,text:'テストメモ1'},{id:2,text:'テストメモ2'},{id:3,text:'テストメモ3'}]"/>
</template>

<script>
import MemoList from './components/MemoList.vue'

export default {
  name: 'App',
  components: {
    MemoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
