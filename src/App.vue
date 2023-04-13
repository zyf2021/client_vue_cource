<template>
    <div class = "app">
    <post-form/>
    <post-list v-bind:posts="posts"/>
        
    </div>

</template>

<script>
import PostList from './components/PostList.vue';
import PostForm from './components/PostForm.vue';


export default {
  components: { PostForm, PostList },
    data() {

        return {
            text: 'trertre',
            title: 'rter',
            posts: [
                {id:0, title: 'Новость 1', text: 'text', likes: 1},
                {id:1, title: 'Новость 2', text: 'text', likes: 4},
                {id:2, title: 'Новость 3', text: 'text', likes: 0},
            ],
        }
    },
    methods: {
        addLike(id){
            this.posts[id].likes += 1;
        },
        addPost(){
            const newPost = {
                id: Date.now(),
                title: this.title,
                text: this.text,
                likes: 0
            }
            this.posts.push(newPost)
        },
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

