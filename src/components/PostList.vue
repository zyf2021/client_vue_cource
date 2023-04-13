<template>
    <div v-show="posts.length > 0">
        <post-item 
            v-for="post in posts" 
            :post="post"
            :key="post.id"
            @remove="removePost(post)"
            @add="addLike"
        />
    </div>
    <h3 v-show="posts.length == 0">Список пуст</h3>
</template>

<script>
import PostItem from './PostItem.vue'
//import MyButton from './UI/MyButton.vue';

export default {
  components: { PostItem },
    props:
    {
        posts: {
            type: Array,
            required: true,
        },
    },
    data() {
        return {
            
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

</style>