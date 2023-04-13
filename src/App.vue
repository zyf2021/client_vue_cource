<template>
    <div class = "app">
    <post-form  
        @create = "addPost"

    />
    <post-list
        @add = "addLike" 
        @remove = "removePost"
        v-bind:posts="posts"
    />
    </div>

</template>

<script>
import PostList from './components/PostList.vue';
import PostForm from './components/PostForm.vue';


export default {
  components: { PostForm, PostList },
    data() {
        return {
            posts: [
                {id:0, title: 'Новость 1', text: 'text', likes: 1},
                {id:1, title: 'Новость 2', text: 'text', likes: 4},
                {id:2, title: 'Новость 3', text: 'text', likes: 0},
            ],
        }
    },
    methods: {
        addPost(post){
            console.log(post)
            post.id = this.posts.length
            this.posts.push(post)
        },
        addLike(id){
            this.posts[id].likes += 1
        },
        removePost(post){
            this.posts = this.posts.filter(p => p.id !== post.id)
        }
    }
}
</script>


<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    .app {
        margin: 20px
    }
    
    
</style>

