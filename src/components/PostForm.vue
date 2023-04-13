<template>
   <div >
        <form @submit.prevent>
            <h1>Создание поста</h1>
            <my-input placeholder="Название"
                      v-model = "post.title"
                      type="text"></my-input> 
            
            <my-input class = "input" 
                   type = "text" 
                   placeholder="Описание" 
                   v-model="post.text"
            ></my-input>
            <my-button @click = "addPost">
                Создать
            </my-button>
        </form>
    </div>
</template>

<script>
export default {
    data(){
        return {
            post: {
                id: 0,
                title: '',
                text: '',
                likes: 4
            }
        }
    },
    methods: {
        addPost() {
            this.post.id=Date.now()
            this.post.likes = 0
            this.$emit('create', this.post)
            this.post = {
                title: '',
                text: '',
                likes: '',
            }
        }
    }
}
</script>

<style>
    form {
        display:flex;
        flex-direction: column;
    }
</style>