<template>
    <div class = "post">
        <div><strong>ID<br></strong>{{ post.id }}</div>
        <p><strong>Название<br></strong>{{ post.title }}</p>
        <p><strong>Текст<br></strong>{{ post.text }}</p>
        <p>Number of likes 
            <strong>{{ post.likes }}</strong></p>
        <div class="post__btns">
            <my-button @click="addLike(post.id)">Like</my-button>
            <my-button
                @click="removePost(post)"
            >Удалить
            </my-button>
        </div>

    </div>
</template>

<script>
export default {
    name: 'post-item',
    props:{
        post: {
            type: Object,
            required: true,
        }
    },
    methods: {
        addLike(id){
                this.$emit('add', id)
            },
        removePost(post){
            this.$emit('remove', post)
        }
    }
}
</script>

<style>
    .post {
        padding: 15px;
        border: 2px solid teal;
        margin-top: 15px;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .post__btns {
        display: flex;
    }
</style>