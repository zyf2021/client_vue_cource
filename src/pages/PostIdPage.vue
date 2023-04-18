<template>
  <div>
    <h1>Страница поста {{ $route.params.id }}</h1>
    <h3>{{ post.title }}</h3>
    <p>{{ post.body }}</p>
    <h6>UserId {{ post.userId }}</h6>
  </div>
  <div 
    v-for = "comment in comments"
    :key="comment"
    :value="comment"
  >
    <h3>email {{ comment.email }}</h3>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return {
      post: {},
      comments: []
    }
  },
  methods: {
    async fetchPost(){
      try {
        setTimeout(async ()=>{
            const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
            console.log(response.data)
            this.post = response.data
          }, 1000)
      } catch(e) {
        alert(e)
      } finally {
        
      }
    },
    async fetchCommentsByIdPost(){
      try {
        setTimeout(async ()=>{
            const response = await axios.get(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}/comments`)
            console.log(response.data)
            this.comments = response.data
          }, 1000)
      } catch(e) {
        alert(e)
      } finally {
        
      }
    }
  },
  mounted() {
    this.fetchPost()
    this.fetchCommentsByIdPost()
  }
}
</script>

<style>

</style>