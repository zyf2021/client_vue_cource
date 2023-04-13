<template>
    
    <div class = "app">
        <h1>Заголовок</h1>
        <my-button
            @click = "showDialog"
        >Создать пост</my-button>
        <my-dialog v-model:show = dialogVisible>
            <post-form  
                @create = "addPost"

            />
        </my-dialog>
        <post-list
            @add = "addLike" 
            @remove = "removePost"
            v-bind:posts="posts"
            v-if = "!isPostLoading"
        />
        <div v-else>Загрузка..</div>
    </div>

</template>

<script>
import PostList from './components/PostList.vue';
import PostForm from './components/PostForm.vue';
import axios from 'axios'

export default {
  components: { PostForm, PostList },
    data() {
        return {
            posts: [
                /*{id:0, title: 'Новость 1', text: 'text', likes: 1},
                {id:1, title: 'Новость 2', text: 'text', likes: 4},
                {id:2, title: 'Новость 3', text: 'text', likes: 0},*/
            ],
            dialogVisible: false,
            modificatorValue: '',
            isPostLoading: true
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
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts(){
            try {
                setTimeout(async ()=>{
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
                    console.log(response)
                    const data = response.data
                    data.forEach(element => {
                        this.posts.push({
                            id: element.id - 1,
                            title: element.title,
                            text: element.body,
                            likes: 0
                        })
                    });
                    this.isPostLoading = false
                }, 1000)
            } catch(e) {
                alert(e)
            }
        }
    },
    mounted() {
        this.fetchPosts();
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

