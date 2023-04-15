<template>
        <div v-show="posts.length > 0">
            <transition-group name="post-list">
                <post-item 
                    v-for="post in posts" 
                    :post="post"
                    :key="post.id"
                    @remove="removePost(post)"
                    @add="addLike"
                />
            </transition-group>
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
    .post-list-item {
    display: inline-block;
    margin-right: 10px;
    }
    .post-list-enter-active,
    .post-list-leave-active {
    transition: all 0.4s ease;
    }
    .post-list-enter-from,
    .post-list-leave-to {
    opacity: 0;
    transform: translateX(100px);
    }
    .post-list-move {
        transition: transform 0.4s ease;
    }
</style>