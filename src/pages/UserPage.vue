<template>
    
    <div>
        <h1>Заголовок</h1>
        <my-input 
            v-model="searchQuery"
            placeholder = "Поиск..."
        ></my-input>
        <div class="app__btns">
            <my-button
                @click = "showDialog"
            >Создать пост</my-button>
            <my-select
                v-model="selectedSort"
                :options="sortOptions"
                @change="methodSelect"
            ></my-select>
        </div>
        
        <my-dialog v-model:show = dialogVisible>
            <post-form  
                @create = "addPost"
            />
        </my-dialog>
        <post-list
            @add = "addLike" 
            @remove = "removePost"
            :posts="sortedAndSearchedPosts"
            v-if = "!isPostLoading"
        />
        <div v-else>Загрузка..</div>
        <div class="page__wrapper">
            <div
                v-for = "pageNumber in totalPages"
                :key="pageNumber"
                class="page"
                :class="{
                    'current-page': page === pageNumber
                }"
                @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
    </div>

</template>

<script>
import PostList from '@/components/PostList.vue';
import PostForm from '@/components/PostForm.vue';
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
            isPostLoading: true,
            selectedSort: '',
            searchQuery: '',
            page: 1,
            limit: 5 ,
            totalPages: 0,
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'text', name: 'По содержанию'},
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
            //let k = 0
            
            for (let k = 0; this.posts.length - 1; k++) {
                if(this.posts[k] === undefined) {return}
                if (this.posts[k].id == id) {
                    this.posts[k].likes += 1
                    console.log('find')
                }
            }
            //this.posts[id].likes += 1
        },
        removePost(post){
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts(){
            try {
                ///this.isPostLoading = true
                setTimeout(async ()=>{
                    const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                        params: {
                            _page: this.page,
                            _limit: this.limit
                        }
                    })
                    this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit)
                    
                    
                    
                    const data = response.data
                    let posts = []
                    data.forEach(element => {
                        posts.push({
                            id: element.id - 1,
                            title: element.title,
                            text: element.body,
                            likes: 0
                        })
                        this.isPostLoading = false
                    })
                    this.posts = posts
                }, 1000)
            } catch(e) {
                alert(e)
            } finally {
                
            }
        },
        methodSelect() {
            console.log(this.selectedSort)
        },
        changePage(pageNumber) {
            this.page = pageNumber
            this.fetchPosts()
        }
    },
    mounted() {
        this.fetchPosts();
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                return post1[this.selectedSort]?.localeCompare(post2[this.selectedSort])
            })
        },
        sortedAndSearchedPosts(){
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },
    watch: {
        /*selectedSort(newValue) {
            console.log(newValue)
            this.posts.sort((post1, post2) => {
                return post1[newValue]?.localeCompare(post2[newValue])
            })
        },
        dialogVisible(newValue){
            console.log(newValue)
        }*/
    }
}
</script>


<style>

    .app_btns{
        display: flex;
        justify-content: space-between;
    }
    .page__wrapper {
        display: flex;
        margin-top: 15px;
    }
    .page {
        border: 1px solid grey;
        padding: 10px;
        margin-inline: 2px;
    }
    .current-page{
        border: 2px solid teal;
    }
    
</style>

